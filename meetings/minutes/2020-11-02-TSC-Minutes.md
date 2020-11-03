# Minutes from the 2020-11-02 Laminas Technical Steering Committee Meeting

- When: 2020-11-02 at 19:00 UTC, until 20:40 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Gary Hockin
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Max Bösing
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Michał Bundyra
  - Rob Allen
  - Witold Wasiczko

Quorum was met (14 out of 15 members were present).

## Agenda

- Commercial vendor program updates? ([jump to discussion](#commercial-vendor-program))

  Updates on the commercial vendor program? Any vote as appropriate?

- Github Actions instead of Travis-CI? ([jump to discussion](#github-actions))

  Github Actions has been, so far, much faster and efficient to set up in repositories all over github.

  While Travis-CI is certainly a good platform that has served us well for many many years, having the ability to create our own github actions may simplify the CI setup for most our repositories.

  The proposal is to:

  - Find an optimal "baseline" Github Actions workflow that we'd like to use
  - Investigate whether there is a way to unify most CI workflows (rather than maintaining them in each repository)
  - Move current Travis-CI configuration to Github Actions workflows
  - Sunset Travis-CI configuration and disable it on the various repositories

- Cache adapters to abandon ([jump to discussion](#cache-adapters))

  With `laminas/laminas-cache` v2.10, all cache adapters are moved to their own satellite.
  Next step would be to abandon some of those packages as we are either dropping support for PHP <7.3 and some adapters never migrated to PHP 7 **or** we just dont want to support specific cache backends anymore.

  The following adapters are currently "available":

  - [APC](https://github.com/laminas/laminas-cache-storage-adapter-apc)
  - [APCu](https://github.com/laminas/laminas-cache-storage-adapter-apcu)
  - [BlackHole](https://github.com/laminas/laminas-cache-storage-adapter-blackhole)
  - [DBA](https://github.com/laminas/laminas-cache-storage-adapter-dba)
  - [ExtMongodb](https://github.com/laminas/laminas-cache-storage-adapter-ext-mongodb)
  - [Filesystem](https://github.com/laminas/laminas-cache-storage-adapter-filesystem)
  - [Memcache](https://github.com/laminas/laminas-cache-storage-adapter-memcache)
  - [Memcached](https://github.com/laminas/laminas-cache-storage-adapter-memcached)
  - [Memory](https://github.com/laminas/laminas-cache-storage-adapter-memory)
  - [ExtMongodb](https://github.com/laminas/laminas-cache-storage-adapter-mongodb)
  - [Redis](https://github.com/laminas/laminas-cache-storage-adapter-redis)
  - [Session](https://github.com/laminas/laminas-cache-storage-adapter-session)
  - [WinCache](https://github.com/laminas/laminas-cache-storage-adapter-wincache)
  - [XCache](https://github.com/laminas/laminas-cache-storage-adapter-xcache)
  - [ZendServer](https://github.com/laminas/laminas-cache-storage-adapter-zend-server)

  We should abandon the following packages:

  - APC
    - it is superseded by APCu and thus not needed anymore
  - Memcache
    - it was dead for almost 7 years
    - Last year, some guys fixed the extension to work with PHP 7+ but its not in active development
  - WinCache
    - Windows (Microsoft dropped support for PHP anyways)
    - there is no-one who can execute tests for this package (not even travis)
  - XCache
    - is dead for years
  - ZendServer
    - there is no-one who can execute tests for this package (not even travis)

- RFCs - discuss directly on GitHub? ([jump to discussion](#rfc-location))

  As [noted by the user on the Laminas Slack](https://laminas.slack.com/archives/C4QBQUEG5/p1602604527127400), our current issue template suggests that new features/RFCs should be posted to the forums for discussion.

  That is quite inefficient, since:

  - the amount of users following the forum is a fraction of the users following our repositories
  - it is one more step for people to contribute

  It could be a good idea to just endorse opening issues as "feature request" or "RFC" instead, since all the Laminas TSC members and community members are quite familiar with PR/issue tooling of GitHub.

## Commercial Vendor Program

James asked for an update on the commercial vendor program.
Matthew W indicated he has been mailing our Linux Foundation legal contact weekly, but with no updates to date.

## Github Actions

Marco added this item to the agenda.
He has noted that builds even for trivial changes can take up to an hour depending on how many pushes are being made across the organization (as we can generally only have 5 concurrent jobs per organization at any given time, and most pushes spawn anywhere from four to 8 jobs).
On top of that, Travis recently [announced a new pricing structure](https://blog.travis-ci.com/2020-11-02-travis-ci-new-billing), which would limit build hours to 1000 per month per organization, which we will likely reach within 2-3 weeks each month.
While we can apply for an OSS exemption, such an exemption is not guaranteed, and could be revoked at any time.

Rob asked if there are limits on GitHub Actions, recalling something about 2000 hours per month. Geert checked, and found that the 2000 hour limit is for private repositories only; OSS repositories have no limit.

Other points brought up:

- We should likely optimize builds to exit early if there are no code changes.
- We need to find out if there are ways to make the actions and/or workflows global, to simplify adding them and keeping them up-to-date ([this may be possible already](https://docs.github.com/en/free-pro-team@latest/actions/learn-github-actions/sharing-workflows-with-your-organization)).
- A single step/action that runs everything would be ideal.
- Parity with `.travis.yml` would be ideal.

Matthew W asked for volunteers to reesarch solutions and develop a plan.
The following people indicated they were interested:

- Matthew S
- Luís
- Gary
- Marco

If others are interested in helping, please contact one of them.

## Cache Adapters

Max has been busy splitting the various laminas-cache adapters into their own repositories, and the upcoming version 2.10 release will now depend on each of the satellite packages.
He has proposed a version 3 that removes them as package requirements, bumps the minimum PHP version to 7.3, and potentially removes several backends, as noted in the TOC.

Luís suggested also removing the session adapter, and potentially any and/or all of the various RDBMS and document database adapters (e.g., DBA, MongoDB).

In the end, we voted on "Do we accept the proposal made by Max around changes to laminas-cache and its satellite packages?"
The vote passed unanimously.
Max indicated that the roadmap will be:

- A version 2.10 created this week.
- A 3.0 version the week of the 16th that also adds PHP 8 support.
- Version 2 releases of individual adapters to make them compatible with laminas-cache v3 and to add PHP 8 support.
  Only adapters we plan to keep will get this version bump.

## RFC Location

Since before we migrated from ZF to Laminas, we asked that RFCs be posted to the Contributors section of our forums.
However:

- We do not have a lot of traffic to the forums.
- The forums are one more place to check around proposed features or changes to a component.
- There is no cross-linking from the forums to GitHub and back.
- The forums require an additional user and profile (though you can use your GitHub account for login).

Marco has proposed we bring them to GitHub instead, potentially as native issues.

Matthew W noted that this will work for the majority of RFCs, which only touch on a single component.
However, for those where they may touch on multiple components (e.g., the CLI initiative, the changes to the event manager and service manager prior to version 3), having another location would be useful.
Andreas pointed out how easy it is to find RFCs with communities that do them in a central location, such as the PHP project or the IETF; he advocated for a central repository for all RFCs.

Matthew W boiled the discussion down to the following requirements:

- RFCs must be on GitHub (facilitates cross-linking, puts them close to the context they describe).
- An RFC issue type plus an RFC label would likely be sufficient.
- For cross-component RFCs, we can use a central repository (either maintainers or TSC), and then create an organization-level project to track tasks.
- We create automation for getlaminas.org to periodially update a listing of RFCs based on retrieving issues on each of our organizations marked with that label.

At this point, we voted on the above.
The vote passed unanimously.
Matthew volunteered to create the issue template and propagate the label to all repos.
**We are still looking for a volunteer to do the RFC aggregation automation.**
