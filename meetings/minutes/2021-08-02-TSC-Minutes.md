# Minutes from the 2021-08-02 Laminas Technical Steering Committee Meeting

- When: 2021-08-02 at 19:00 UTC, until 21:38 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl (left shortly after 20:00)
  - Frank Brüchner
  - Luís Cobucci (left shortly after 20:00)
  - Marco Pivetta
  - Matthew Setter (started shortly after 20:00)
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra

Quorum was met (8 out of 15 members were present were present at any given point).

## Agenda

### Fund Sury repository 8.1 pre-RC builds

[Matthew](https://github.com/weierophinney) notes that in conversations with Ondrej Sury (author and maintainer of the Sury Debian repository for PHP, on which our CI is built), Ondrej indicated that he will not offer PHP 8.1 builds until the first RC, unless somebody is willing to pay for the work.
Matthew is curious if we should put Laminas Project funds towards this effort.

Marco wondered if any of the funding would be going towards a TSC member or Laminas Project maintainer assisting with the work.
Matthew indicated that no, it would only go towards the Sury repository owners and maintainers.
Marco indicated that while he's 100% for sponsoring OSS, he feels it doesn't work when it's OSS funding OSS; a smaller amount money is just getting shuffled around at that point.
We asked Ben Ramsey, who was attending the meeting at this time, and is one of the release mananagers for 8.1, when the RC would occur, and he pointed to a document that indicates 2021-09-02 as the target for RC1.

Max pointed out that the shivams PHP builder for GHA could likely be re-used by us, and would allow us to work on our own schedule instead of that of the repository owner.
Matthew was worried that build times of our CI container would jump into the hours if we did this, versus the 10 minutes or so they currently take.
Marco jumped in to say that he's done a lot of work with docker build caches in recent months, including on GHA, and we could likely reduce the amount of time to build even from what it currently is using those approaches.

Consensus:

- We will not fund the Sury repository for this effort.
  Worst case scenario is that we are able to use RC1 within 5 weeks.
- We will work on using the shivams PHP builder in our container build pipeline to allow us to build new PHP versions on our own schedule.

### Allow PHP-Assert along with Webmozart-Assert in Specific Cases

[Maximilian Bösing](https://github.com/boesing) wants to talk about the usage of `assert` (PHP) and `Assert` (Webmozart) when providing types for psalm.
In some cases, having runtime assertions may consume unnecessary opcodes just to provide proper psalm-types.

Lets assume the following code:

```php
$foo = sprintf('foo bar baz %d', 1);
assert($foo !== '');
```

Psalm is not able to verify that `$foo` is a non-empty-string, even though the first argument is a non-empty-string and therefore, the return value must either be `false` (in case of an error) or `non-empty-string`.

- https://psalm.dev/r/add6e2b321

Max prefers using `assert($foo !== '')` over `Assert::stringNotEmpty` to avoid redundant runtime checks which actually only have to be made to "make psalm happy".
As we do want to "make psalm happy", we can either use the `@psalm-var` inline-annotation, use `assert` or use `@psalm-assert` (as provided by webmozart `Assert`).

The first two options do not execute runtime checks (`assert` won't on production system as `zend.assertion` supposed to be `-1`). The webmozart assertion will execute assertions even though the assertion will always succeed.

Max prefers having `assert` over `@psalm-var` here, as it may fail in unit tests (or on non-production systems) and thus, the assertion will still be verified and not just assumed.

**Questions:**

- Do we want to use `assert` in some cases?
- If the answer to the first question was yes, how can we provide "rules" for doing so, so we can put these in the contributors guide?
- If the answer to the first question was no, do we want to require runtime `Assert` (webmozart) checks or do we accept inline `@psalm-var` annotations?

Marco jumped in at this point out that what we call "assertions" is sometimes:

- expectations of something that is always supposed to be true (assumption), for which `assert()` is safe to use, as it's a "hint" and a runtime check in  dev mode
- expectations of some input to follow some rule, in which case it is NOT a dev-only concern, and therefore  `assert()` cannot be used, and `Assert::...`  is needed

Max indicated that the former was what spurred his question; he had scenarios such as `max(10, 25)` that Psalm would not infer would result in a positive integer or `sprintf('foo%s', …)` that would not be matched as a non-empty string.
Marco said that yes, these are perfectly good scenarios for using `assert()` instead of `Assert::...`.

Since we had consensus, Matthew asked for a volunteer to write up some notes for the contributor's guide.
Luís volunteered.

### Locked Dependencies for All Supported PHP Versions

[Maximilian](https://github.com/boesing) wants to talk about the current CI matrix.

Lately, we encountered some issues with different 3rd party libraries due to the fact that these are way more strict in dropping PHP versions along with major bumps.

This makes it almost impossible to have a `composer.lock` which will be valid for **all** PHP versions (`7.3`, `7.4`, `8.0` so far).

Some packages where it would be impossible to have a proper `composer.lock` for all supported versions (without dropping support for these versions and/or swapping to alternatives):

| Package | Major Version | PHP constraint
|---------|------------|--------
| [maglnet/composer-require-checker](https://github.com/maglnet/ComposerRequireChecker) | 2.x | `^7.2`
| [maglnet/composer-require-checker](https://github.com/maglnet/ComposerRequireChecker) | 3.x | `^7.4 \|\| ^8.0`
| [ocramius/package-versions](https://github.com/Ocramius/PackageVersions/) | 1.5.1 | `^7.3`
| [ocramius/package-versions](https://github.com/Ocramius/PackageVersions/) | 2.0 | `^7.4.7`
| [ocramius/package-versions](https://github.com/Ocramius/PackageVersions/) | 2.1 | `^7.4.7 \|\| ~8.0.0`

For `ocramius/package-versions` we already had to switch to `composer/package-versions-deprecated` to get some of our components up and running with the current matrix.
That's all due to the fact that we need one single `composer.lock` to fit for all PHP versions.
This will become more and more a problem when projects start to drop old PHP versions.

So we have two options:

1. drop support of PHP version as soon as 3rd-party libraries we are using drop support for these versions
1. only use `locked` dependencies for the stable version marked by the `dev.laminas.org` API which is requested in the matrix generation(?) and for all other versions, use `lowest` or `latest`

The latter will work with the [recent suggestions](https://gist.github.com/weierophinney/b003e50c3c2667d08076caf31ebd36a4) of [Matthew](https://github.com/weierophinney) regarding the migration to GHA.
That guide says:

> Using PHP 7.4, run composer update

So even though the component had support for PHP 7.3, some packages might be ended up having a `.laminas-ci.json` with these contents:

```json
{
    "exclude": [
        {"name": "PHPUnit on PHP 5.6 with locked dependencies"},
        {"name": "PHPUnit on PHP 7.0 with locked dependencies"},
        {"name": "PHPUnit on PHP 7.1 with locked dependencies"},
        {"name": "PHPUnit on PHP 7.2 with locked dependencies"}
    ]
}
```

This said, there should be no reason why we need `locked` dependencies for all PHP versions.

We had a ranging discussion around why we use the lockfile at all (helps us identify when we adopt features not in the lowest supported version, or a later version causes breakage), and why non-testing tooling requires a lockfile (tools are generally too brittle).
In the end, we decided the following:

- Generate the lockfile using the minimum PHP version the package supports.
- Run unit tests against all supported PHP versions using lowest and latest dependencies.
- Run unit tests against lowest supported PHP version using lockfile (if present).
- Run QA tooling against lowest supported PHP version using lockfile.

We decided that this is not a BC break per se; it just changes the matrix that is being used.
As such, we can do it for a new minor version.

### Remove `laminas/laminas-zendframework-bridge` dependency from our packages

Over the past few weeks, we received multiple reports of people requesting us to drop `laminas/laminas-zendframework-bridge`
from our packages.

Our (TSC) response so far has been that we cannot do this until a new major version is released.
The reason for such a response is that people still rely on `Zend\` classes in their codebases, and therefore removal of `laminas/laminas-zendframework-bridge` could constitute a BC break for them, when a `laminas/` package substitutes a `zendframework/` one.

There may be a better solution to this though, which allows removal in a new **minor** release.

Here's an example for a hypotetical `laminas/laminas-xyz` package:

1. Remove the `{"replace": {"zendframework/zend-xyz": "self.version"}}` `replace`: block from `composer.json`:

   ```diff
   {
       ...
   -    "replace": {
   -        "zendframework/zend-xyz": "self.version"
   -    }
   }
   ```

2. Add a `conflict` with the old package in `composer.json`:

   ```diff
   {
       ...
   +    "conflict": {
   +        "zendframework/zend-xyz": "*"
   +    }
   }
   ```

3. Remove the `laminas/laminas-zendframework-bridge` dependency:

   ```diff
   {
       ...
       "require": {
           ...
   -        "laminas/laminas-zendframework-bridge": "^1.0"
       }
   }
   ```

4. Release under a new **minor** version (the `y` in `x.y.z`)

The proposed approach allows us to get a clean upgrade path for people that already use `laminas/*` packages, and already migrated away from the abandoned `zendframework/` packages.

People migrating from `zendframework/*` packages to `laminas/*` will still be able to use earlier **minor** releases of `laminas/*`, which we did release with the compatibility layer enabled.

Marco mainly wanted to see if we saw any holes in the proposal, or if we could go ahead and start on this effort.
Michał noted that 2/3 of package installs are now Laminas, so this is likely the right time to move forward.
His main concern is if the existing package versions would still get support.
Matthew and Marco pointed out that as long as those versions have minimum PHP versions still getting security support, they'll get security patches.

The other concern Michał brought forward was that the original plan was to remove the bridge for the next major version; that the current major version should retain backwards compatibility, and thus allow upgrading when replacing a ZF package.
Marco and Matthew noted that the problem with this is that it forces a new major version just to remove the bridge, when there may be no compelling reason to do so otherwise.
On top of that, providing the ZF package is not a contract, and falls more in line with PHP version support, which we allow removing in new major versions.

While there were a number of potential problem scenarios brought forward, in all cases, the consensus was that the user would either get an install with the bridge on an earlier version, or the latest version without the bridge; the latter would only happen if no ZF dependencies were defined in 3rd party packages that would force a lower version to be installed.

In the end, we decided to move forward with this first in laminas-stdlib, and announce the proposed change via the blog when we do to ensure we get feedback from users.

### Require `GITHUB_TOKEN` permission to be explicitly specified in GHA workflow files

Permissions for `GITHUB_TOKEN` are [too broad and provide write access to a number of scopes](https://docs.github.com/en/actions/reference/authentication-in-a-workflow#permissions-for-the-github_token) when action is run in a privileged context of a maintainer. Such privileged context is invoked, for example, on branch push event after the PR was merged. This poses a security risk in case of supply chain attack or vulnerability in invoked dependencies (eg [CVE-2021-29472 for Composer](https://nvd.nist.gov/vuln/detail/CVE-2021-29472))

I propose to make [permissions](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#permissions) field mandatory in all workflow files in all Laminas repositories with only required privileges specified for the specific workflow.

> ```yaml
> permissions:
>   actions: read|write|none
>   checks: read|write|none
>   contents: read|write|none
>   deployments: read|write|none
>   issues: read|write|none
>   packages: read|write|none
>   pull-requests: read|write|none
>   repository-projects: read|write|none
>   security-events: read|write|none
>   statuses: read|write|none
> ```

When Matthew asked for an example of problem behavior that can arise, Aleksei noted the possibility of a `composer ` install script that could push commits to the repository as a potential vector.
Marco and Matthew then noted that this might be something to bring up to the GitHub security team, as that becomes non-trivial to potentially exploit, and would be a reason to recommend more stringent permissions as the defaults for workflows.

We decided to table the discussion so that Aleksei can do more research, and notify GitHub if necessary.
