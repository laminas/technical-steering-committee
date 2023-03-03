# Minutes from the 2023-01-09 Laminas Technical Steering Committee Meeting

- When: 2023-01-09 at 19:00 UTC, until 20:32 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl (joined at the 30 minute mark)
  - Frank Brückner
  - Gary Lockett
  - George Steel
  - Maximilian Bösing
  - Matthew Weier O'Phinney
  - Michał Bundyra

Quorum WAS met (9 out of 15 members were present).

## Agenda

### PSR-11 v2

Max wanted to discuss the fact that Laminas lacks support for psr/container v2 and how we can move forward.
Due to the fact that laminas/laminas-servicemanager provides the base for plenty of components (listed below), that change will have a huge impact PLUS providing a compatible version for psr/container v1 AND v2 in the same time is almost impossible.
There might be even a v3 on the road where `mixed` type is being added as the return type of `ContainerInterface#get` and thus, it might be helpful to reach out to the PSR-11 maintainer to see if there are already plans for that.
Given the fact, that its impossible to provide a version for both container v1 and v2, that would mean a new major version for laminas-servicemanager and thus, new major versions for all the components (listed below).

**Questions**

- Do we want to create a new major version which only supports `psr/container` v2?
- Do we want to create new major versions for all the components relying on `laminas/laminas-servicemanager` and/or is there a component where a new major versions is almost finished?

Creating new major versions of those components need to orchestrated as some projects might depend on each other as well:

| Component                                 | Details                                                                                                                                                                                                                                                               |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `laminas/laminas-validator`               | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-mvc`                     | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-feed`                    | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-view`                    | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-text`                    | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas-serializer`                      | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version. :warning: does not have a requirement to any servicemanager version and thus projects might potentially get BC breaks here.                        |
| `laminas/laminas-router`                  | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-log`                     | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-inputfilter`             | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-i18n`                    | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-hydrator`                | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-form`                    | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-filter`                  | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-cache`                   | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-barcode`                 | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-cache-storage-adapter-*` | Only provides servicemanager wiring for `laminas-cache`. :warning: `laminas-cache` new major version needs to be supported as well.                                                                                                                                   |
|                                           | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
|                                           | Implements a `PluginManager` and thus needs code-changes and can only support the latest `servicemanager` version.                                                                                                                                                    |
| `laminas/laminas-session`                 | Only provides servicemanager wiring and thus can add support for v3 & v4                                                                                                                                                                                              |
| `laminas/laminas-crypt`                   | :warning: This component has still a dependency to servicemanager while it is not using it anymore.                                                                                                                                                                   |
| `laminas/laminas-test`                    | Only uses servicemanager for unit test stuff and thus can add support for v3 & v4                                                                                                                                                                                     |
| `laminas/laminas-mvc-i18n`                | Only provides servicemanager wiring and thus can add support for v3 & v4                                                                                                                                                                                              |
| `laminas/laminas-developer-tools`         | Consumes MVC methods and uses `servicemanager` to retrieve data and thus can add support for v3 & v4                                                                                                                                                                  |
| `laminas/laminas-mvc-plugin-identity`     | Provides Only provides servicemanager wiring and thus can add support for v3 & v4                                                                                                                                                                                     |
| `laminas/laminas-mvc-middleware`          | Does not have a direct dependency to the servicemanager and thus could simply remove the dependency. `laminas-mvc` `Application#getServiceManager` is being used and thus it might be the reason why the servicemanager is required. Can add support for v3 & v4 tho. |
| TBD                                       | :warning: there are plenty of other components not yet listed in this table. In case we are fine with going that way, I'll complete this list to outline the full scope.                                                                                              |

#### Discussion

Max notes that supporting both versions of psr/container is not possible, as class aliasing breaks any package pinned to a different version than the one installed.

Matthew then noted the intended approach from the FIG side of the equation:

- FIG releases a new MINOR version that adds parameter type-hints only.
  This is considered backwards compatible with existing implementations, as _widening_ a parameter type in an implementation fulfills LSP rules.
  Implementations MAY add return type hints at that point if desired, as that also fulfills LSP rules (return types of implementations are allowed to be narrower than the parent implementation).
- FIG releases a new MAJOR version that adds the return type-hints.
  This is a breaking change, because if an implementation has not yet defined return type-hints, they will now no longer comply.

While with a number of our PSR implementations we have added return type hints, we cannot add parameter type hints as doing so will be a BC break for anybody extending our own implementations, so adopting a v2 of any FIG specification automatically requires a new major.

As Max notes, any component that implements a laminas-servicemanager PluginManager is automatically affected, and then this has ripple effects on any component that depends on _those_ components.
His concern is that this will be a difficult upgrade for users, with the potential for a lot of breakage.

Several folks chimed in at this point that users would need to opt in to new major versions when doing updates; a `composer update` won't update from version 3.4 to version 4.0 automatically (unless you do something crazy like use the `*` constraint).
Max suggested there may be some cases where laminas-servicemanager is a transitive dependency, not an explicit one, and this would be where he expects an issue.
Several folks noted that in these cases, you still need to pass the `--with-dependencies` option when performing an update, and that Composer will not bump to a new major of a transitive dependency in that case.
As such, declaring new majors to adopt v2 support of a PSR package is the safest way to go regardless.

Matthew pointed to the v2 -> v3 migration, and suggested that Max work on v4, and identify any issues or improvements we can make to v3 to facilitate forward migration.
This would also allow us to do some previously identified cleanups: removal of initializers, removing legacy factory interfaces, etc.
Additionally, we may want to mark v3 as LTS when this happens, to give a defined time period for consumers to update.

Aleksei suggested that this might be a good time to separate the plugin manager definition from laminas-servicemanager, and create a package specifically for that.
Max doesn't seem to think this is necessary, and countered with a proposal that any package that has a plugin manager split that functionality out to a subpackage `laminas-<component>-servicemanager` that would define the plugin manager and the component registration.
If the components internally consume the plugin manager, type-hints could be updated to the PSR-11 interface instead, which would allow shipping hard-coded implementations for standalone usage.
(Alternately, they could provide a PSR-11 interface extension that has a defined return type to the `get()` method.)

#### Decisions

- We agreed that a new major is required here.
- We agreed that Max would create a project to track all the pieces (changes to laminas-servicemanager, components that need updates).
- We agreed that we should likely create new subpackages for any package currently shipping any plugin managers, so that the laminas-servicemanager-based plugin manager implementations can be opt-in.
- We agreed that laminas-servicemenager v3 should receive 12 months of LTS after v4 is released.
  LTS would include security fixes and potentially Psalm fixes.

### The future of `laminas-api-tools`

Since laminas-mvc seems to be almost dead in favor of Mezzio, laminas-api-tools makes no sense anymore.
There were plans to migrate laminas-api-tools to Mezzio, which would include:

- rewriting the whole admin interface functionality
- adapting plenty of code to work with PSR-7 & PSR-15
- etc.

Since these changes have to be a new major version PLUS there can't be any migration path (as `laminas-mvc is too far away from Mezzio), the rewrite would only provide a "new" laminas-api-tools just for Mezzio.

[Aleksei](https://github.com/Xerkus) already pointed out that there are better projects out there (explicitly mentioned API platform) and thus a new laminas-api-tools platform would be both very time-consuming due to the refactoring (to make it compatible with Mezzio) while not beneficial for projects which are already using laminas-api-tools.

Therefore, the rewrite of laminas-api-tools will be only consumed in new projects starting fresh.

Does Laminas continue the work on laminas-api-tools or should it be abandoned in favor of API platform?

Kinda related: Should Laminas focus on its core components + Mezzio until there are more maintainers available?
To be discussed: What are/should be the core components?

#### Discussion

Gary indicated he's not a fan of API Platform, and would like a Mezzio alternative.
(We discussed the Mezzio alternative off-and-on, interspersed with the other discussions.)

Matthew indicated he is torn, as he knows of a fair number of Zend customers who still use it.
That said, he also pointed out:

- laminas-db as a dependency essentially kills the project, as it is considered "security only".
  We will need to rewrite the RDBMS layer in order to get any new features or fix a number of bugs, and this is a major undertaking.
- Only 2-4 folks in the TSC have deep knowledge of the project, and only Matthew has deep knowledge of the UI, and none of these people has time to dedicate to it.

Max asked what makes laminas-api-tools relevant.
Matthew answered that from a consumer standpoint, the ability to point to a database table, define constraints, and add authn/authz from the GUI, and have everything "just work".
In particular, this is hugely powerful for unsophisticated users, those with little API background, or companies that haven't budgeted much time or money into API development but who nonetheless need something.
This allows quickly creating APIs, and thus business value, for an organization.

Aleksei noted that there are a number of commercial and OSS tools that can do many of these things now, and most are more feature rich.

The key point brought up during the discussion is that users want us to continue maintaining it, but we do not have the resources to do so.
Further, adoption is decreasing dramatically, while we're seeing increasing numbers of installs in our other projects.
Max noted that the admin UI package has only been installed 200k times since we switched the project over to the LF, while Mezzio has 1.3 million installs and laminas-mvc 8.5M.
(Matthew noted that 200k is still a lot, but also conceded the point that it's a decreasing share.)
Matthew also noted that when we release laminas-servicemanager v4, we likely won't want to or be able to update laminas-api-tools anyways, which will leave it behind sooner rather than later.

IF we were to work on API tooling for Mezzio, it would make more sense to focus on key features.
We already have, with mezzio-problem-details, mezzio-hal, and mezzio-(authentication|authorization).
We can look into whether specialized skeletons, code generation, and other features might make it more attractive and easier to use.

#### Decisions

We held a vote, asking whether to mark laminas-api-tools security-only, with the following results:

- 8 people voted to stop maintaining laminas-api-tools
- 2 people abstained

As we needed 50% of all TSC members to vote in favor, the motion carried, and we will discontinue maintenance of laminas-api-tools beyond security patches.
