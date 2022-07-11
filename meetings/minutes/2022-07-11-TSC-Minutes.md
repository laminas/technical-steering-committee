# Minutes from the 2022-07-11 Laminas Technical Steering Committee Meeting

- When: 2022-07-11 at 19:00 UTC, until XX:YY UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Matthew Setter
  - Max Bösing
  - Michał Bundyra

Quorum WAS met (11 out of 14 members were present).

## Agenda

### Future of the migration layer

We should think about how to proceed with `laminas/laminas-dependency-plugin` and `laminas/laminas-zendframework-bridge`.
Due to the latest issues reported in the zendframework bridge (https://github.com/laminas/laminas-zendframework-bridge/issues/95 https://github.com/laminas/laminas-zendframework-bridge/pull/94) and the recent movement of composer not following semver anymore, archiving both `laminas/laminas-dependency-plugin` with `laminas/laminas-zendframework-bridge` might be considered as the best option.

Abandoning old migration stuff after 2.5 years might be okay.

So questions are:

- Should we abandon both packages?
- What components do still rely on the bridge?
- Should we release a new version of these components relying on the bridge so they're not blocking upstream projects getting rid of the bridge?

#### Discussion

Marco immediately jumped in and suggested we mark the repos security-only until we drop 7.4 on our repositories, and noted that we don't need to archive them, just mark them security-only.
Matthew W. noted that he speaks to customers at Perforce weekly that are preparing ZF to Laminas migrations; the need for migrating isn't going away anytime soon; he wanted to know what Marco's rationale was.
Marco noted that he feels "Composer, as a library, is no longer fertile/stable ground for development.
As we proceeed in the next months/years, it will become increasinly complex to keep up with its internals, as BC is broken without respecting semver."

Matthew W. then asked if we should then recommend that users migrating to Laminas who still have need of these plugins use the Composer 2.2 LTS.
Marco and others agreed this was a sane path.
Matthew W. asked if there's a way to pin to a specific minor version of the `composer-plugin-api`; nobody knew, so he said he'd look into it. following the meeting.

#### Decision

At this time, we held a vote, and the decision was to mark the two plugins as security-only; Matthew W. will see if we can pin to specific Composer plugin API versions before doing so.

### Possibilities for project backers

In the early TSC-meetings the funding of the project as well as possibilities for backers were discussed.
A thing I (editor's note: [Andi Rückauer](https://github.com/arueckauer)) remember, but cannot find in the minutes, was some idea project backers to be listed in some form on the website.
Maybe it was in connection with a list of "official" agencies providing support.

The topic has not been discussed recently.
I would like to know if there are any news on this?

#### Discussion

Matthew W. noted that he has dropped the ball on this one.
James Titcumb had volunteered to write-up the policy we agreed to last year for the website, and then Matthew was going to get TSC approval and add it to the website.
At some point, Matthew stopped bugging James about it, so it was dropped.

Andi noted that his company is planning on making a donation, and having some visibility from that would help them in hiring, as there is enthusiasm to work on and sponsor open source.

Matthew W. promised to have something in front of the TSC before next meeting.

### Composer v2

Composer [v2.0.0](https://github.com/composer/composer/releases/tag/2.0.0) was released on end of October 2020.
Since then, the usage of `ocramius/package-versions` became obsolete and therefore, `composer/package-versions-deprecated` was already used to "override" `ocramius/package-versions`.

Due to Marco's amazing idea of providing runtime information for composer dependencies, Composer added this as a native feature with v2.0.0.

However, we do still depend on the `composer/package-versions-deprecated` dependency as it does support PHP 8.0 and PHP 8.1 in the v1.x range while `ocramius/package-versions` would also require the v2+ version of it.
In components which do support PHP 7.4 + PHP 8.0, we are forced to use the composer replacement.

We do have two options as of November this year:

1. Remove PHP 7.4 support, remove `composer/package-versions-deprecated` and re-add `ocramius/package-versions` since it supports PHP 8.0 as of v2.
2. Remove `composer/package-versions-deprecated` and require `composer-runtime-api` v2.
   This will ensure that we can use `Composer\InstalledVersions` without the need of any 3rd-party component.

**Question is:** Do we want to start requiring Composer v2 in our components when it comes to features like `Composer\InstalledVersions`, or should we still allow Composer v1 even if we started to drop Composer v1 in our composer plugins?

#### Discussion

Marco and Max both noted that they would prefer to depend on Composer; it removes the need for an additional dependency, and having the solution backed into package management simplifies the solutions we were using this for.
The main concern from others is whether or not Composer v2 usage is dominant at this point.
Geert noted that v2 was released around 2 years ago, and Luís noted the Packagist install statistics for the composer/compser package as demonstrating that the inflection point for v2 was some time ago.
Max then noted that if a project still relies on Composer v1, they likely are using older versions of Laminas packages anyways.
Marco noted that with v2 supporting as far back as PHP 5.4, there's really no reason NOT to upgrade to Composer v2 at this point.

Aleksei asked where we use the functionality.
Max quickly prepared a list:

```text
laminas/automatic-releases/composer.json:        "ocramius/package-versions": "^2.3.0",
laminas/laminas-cli/composer.json:        "composer/package-versions-deprecated": "^1.11.99.4",
laminas/laminas-servicemanager/composer.json:        "composer/package-versions-deprecated": "^1.0",
mezzio/mezzio-skeleton/composer.json:        "composer/package-versions-deprecated": "^1.10.99",
mezzio/mezzio-swoole/composer.json:        "composer/package-versions-deprecated": "^1.11",
mezzio/mezzio-tooling/composer.json:        "composer/package-versions-deprecated": "^1.11",
```

As Marco noted, most of these have to do with CLI tooling
In some cases, we do it to detect specific package versions in order to provide polyfill support, with the recent FIG evolving versions being a prime scenario where just looking at signatures doesn't work.

#### Decision

At this time, we held a vote, and the decision was to adopt Composer v2.
Max volunteered to spearhead the effort.

### New Laminas maintainers

[Marco Pivetta](https://github.com/Ocramius/) vouches to include following people in our TSC roster:

- [George Steel](https://github.com/gsteel/)
- [Gary Lockett](https://github.com/internalsystemerror)

#### Discussion

George and Gary have been triaging issues, reviewing pull requests, and providing quality patches each for at least a year.
About the only discussion that happened was whether or not they were informed of their nomination before the meeting (they were!), and whether or not we may want to remove some existing members who have been inactive for some time (we likely should).

#### Decision

Please extend a hearty welcome to each of Gary and George, our newest TSC members!

## Next meeting

Our next meeting will be held Monday, 1 August 2022, at 19:00 UTC.
