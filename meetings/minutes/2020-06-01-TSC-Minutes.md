# Minutes from the 2020-06-01 Laminas Technical Steering Committee Meeting

- When: 2020-06-01 at 19:00 UTC, until 20:53 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brückner
  - Gary Hockin (left early)
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Max Bösing
  - Michał Bundyra
  - Rob Allen (left early)
  - Matthew Weier O'Phinney

Quorum was met (11 out of 14 members were present).

## Agenda

- **mezzio-cors library** ([jump to discussion](#cors-library-for-mezzio))

  Max [@boesing](https://github.com/boesing) created an [Expressive module](https://github.com/boesing/zend-expressive-cors)
  which can be used to provide proper CORS details to browsers.
  
  In 2017, he contributed to the MVC module
  [zfr/zfr-cors](https://github.com/zf-fr/zfr-cors/pull/43) to provide per-route
  configuration for CORS. As there is no such library which allows project and
  per-route configuration for CORS in mezzio applications, we might want to move
  it to the mezzio organization.

  **Questions in case we move it to the mezzio organization**

  - The library uses `options.defaults` in route configuration. Should we change
    it to `options` instead to keep request attributes clean?

- **Mezzio Project - Update** ([jump to discussion](#mezzio-project-updates))

  Create new project to track progress with mezzio components.  Set the fixed
  date: 1st of Dec, 2020 (PHP 7.2 has security only support until 30th of Nov,
  2020).

  Update all mezzio components:
  - drop support for PHP prior to 7.3
  - add PHP 7.4 build with lowest and latest dependencies
  - add phpstan or psalm
  - update all dependencies to latest version and drop previous versions
  - solve PHPUnit warnings in tests (support only PHPUnit ^9.1)
  - update to LCS v2 (need to be released before)
  - review all open issues and PRs, reply, close or address with new minor/bugfix
  - report tickets for new major (if there is deprecated functionality which
    should be removed etc)
  - rewrite existing commands to use laminas-cli (keep current commands and mark
    them deprecated)
  - write new commands or at least reports tickets what commands we should add
    in each component and link to laminas-cli project

  Order of update does matter, so we can pin latest versions in skeleton/mezzio.

  - Do we want to do this?
  - Can we achieve it?
  - Any other suggestions?

- **Vote on new members:** ([jump to discussion](#voting-on-new-members))
  - [Matthew Setter (@settermjd)](https://github.com/settermjd) (nominated by Aleksei)

- **Laminas/Mezzio Release Cycle** ([jump to discussion](#release-cadence))
  
  [Max](https://github.com/boesing) would like to talk about what release cycles
  we might want to achieve.
  
  These are the release cycles of other frameworks:
  
  - Symfony:
    Time-based release cycle every 6 months (May/November).
  
  - Yii:
    Extension releases (not quite sure what that is tbh) are tagged on a weekly-base.
    Framework itself is tagged once a month.
  
  - Drupal:
    Release windows depending on release.
    Key dates are on a monthly base.
  
    - First wednesday of every month for bugfix releases
    - Third wednesday of every month for security releases
  
    There are merge windows for new releases.
  
  - Laminas/Mezzio:
  
    Max did not research every repository. However, in the laminas-http
    repository, which is required by the most-installed laminas-mvc package,
    there are a few bugfixes pending since january/february 2020.
  
    For example:
    - [laminas/laminas-http#31](https://github.com/laminas/laminas-http/pull/31)
    - [laminas/laminas-http#34](https://github.com/laminas/laminas-http/pull/34)

    Max accidentally opened up a bugfix which was already patched back in
    february but not released end of may.

    Therefore, treat this as a RFC for a laminas release cycle which allows
    users to have their own contributed fixes in a frustration-free timeframe.
    If we have fixed release cycles for minors/bugfixes, I think its easier to
    take time to focus on those releases instead of doing this besides other
    stuff.

    I kinda like the release cycle of drupal which includes fixed dates so one
    can focus on releasing maintained packages. I see the problem that one
    might be not available at that time (e.g. holidays, ...) but there ain't
    new versions for every package every month *and* there might be always
    someone of the TSC who probably can step in for that special case.

    I am not that familiar with release cycles and thus like to hear what the
    others have to say about this. 

- **laminas-cache "going public"** ([jump to discussion](#laminas-cache))
  
  Splitting laminas-cache into satellites makes progress. Actually, there is a
  new repository `laminas-cache-storage-adapter-template` which can be used as a
  blue-print for new adapters aswell as a `laminas-cache-storage-adapter-test`
  which contains the following classes:
  
  - `LaminasTest\Cache\Storage\Adapter\AbstractAdapterTest`
  - `LaminasTest\Cache\Storage\Adapter\AdapterOptionsTest`
  - `LaminasTest\Cache\Storage\Adapter\CommonAdapterTest`
  
  These are necessary to move the unit tests into the satellites aswell.
  
  To move forward, we have to make those packages publicly available on
  packagist for further development.  Those packages are actually created as
  private packages inside [@boesing](https://github.com/boesing) projects but
  should be moved to laminas project to take on with implementing those packages
  in the satellites.
  
  If there are other ways, please let Max know.

## TSC Activity

Matthew opened with a non-agenda item:

> So, I'm hearing grumbling from a variety of places, and it comes down to this:
> we're not getting a lot of MAINTENANCE activity or help with new features. We
> have a few really active people, and that's it.
>
> We need more people helping on a day-to-day basis.
>
> That means US, folks. And that can be actually reviewing issues and patches,
> merging and releasing, or RECRUITING people to maintain components/subprojects.
>
> But it NEEDS to happen.
>
> And I'm reluctant to vote on most of the agenda this month unless we can get
> some commitments.
>
> [ ... ]
>
> What sorts of commitments can each of [us] provide?

What followed was a lengthy discussion around the availability of different TSC
members, and what obstacles exist that make contributing harder. Many members
agreed to schedule some hours each week for working on the project, with an
emphasis on issue triage; one or two groups were created so that several can
work together at the same time.

One thing identified as an obstacle to both contribution as well as merging and
releasing was that we never brought the `MAINTAINERS.md` guide over from the
Zend Framework repositories, nor the CLI tooling we'd created. Abdul quickly
created a PR to bring the `MAINTAINERS.md` guide over, and we'll address the
tooling later...

...largely because we also started discussing workflows. Rob noted:

> At some point, it felt like merging a PR was a very long list of items to do
> with many possible places to screw up. I don’t know if it’s changed, but for
> someone who was doing it infrequently, it was a massive barrier.

Marco indicated he has a ton of automation around Doctrine and other
repositories he maintains that he could provide to the project, but it would
also require some changes to our workflow: instead of a master branch targeting
bugfixes and a develop branch targeting new features, we would do merges against
either a release branch (bugfixes) or master (features), and use milestones to
control when a release is made. With the automation used by Marco, he indicates
he does most review, merging, and releases from in-browser, using GitHub's merge
button.

We all agreed that a simpler workflow would make attracting new maintainers
easier, and our own jobs easier as TSC members, so Marco and Luís agreed to get
us the automation and instructions. Matthew agreed to develop a plan for rolling
it out across all repositories once its received.

Marco pointed us to the [Behat documentation for his release
automation](https://github.com/doctrine/automatic-releases/blob/master/feature/automated-releases.feature)
so we can decide how we might tweak or alter it to fit our needs.

Matthew the asked how we can hold each other accountable for activity on the
project. Marco indicated he and the group that self-organized have a weekly
calendar entry. Matthew agreed to start tagging Gary with issues he might be
able to help with (CLI tooling, documentation, issue triage). Luís asked if we
could create projects for some of these tasks, and Matthew pointed him to the
[Laminas organization projects](https://github.com/orgs/laminas/projects) that
already exist. Matthew promised to schedule office hours and publicize them, so
that others who want to work collaboratively know times when he's guaranteed to
be available. Gary agreed to do some blogging as well, as documentation and
marketing are also key activities to the project health.

### Synopsis

We all agreed that we need more activity amongst TSC members. The hope is that
with some workflow streamlining, active scheduling on the part of members to
work on issues, and some occasional nudging, we can demonstrate to the
community that the project is alive and kicking - and hopefully attract more
developers to both use and contribute.

Michał and Frank also emphasized that we need to prioritize issue triage, as
determining if an issue is valid or not is often the most important step;
merging is usually the last and easiest task. And for those doing issue triage
or reviewing patches, the most important thing is having the courage to make a
decision. Waiting indefinitely usually means nothing happens.

## Voting on new members

We had one nomination for a new TSC member, [Matthew
Setter](https://github.com/settermjd). The vote to accept
him as a TSC member passed; please welcome our newest member!

## CORS library for Mezzio

Max had written a library some time ago, zend-expressive-cors, to provide CORS
(Cross Origin Resource Sharing) header support to what is now Mezzio. The
library provides integration with mezzio-router in order to provide preflight
responses. He requests bringing it into the Mezzio organization as mezzio-cors.

The vote to accept the new component passed; we will be bringing the new
mezzio-cors component into the Mezzio organization in the coming days or weeks.

## Mezzio project updates

Michał had brainstormed a list (in the agenda, above) of improvements to the
Mezzio libraries. Most of these are around QA tasks: adopting Laminas Coding
Standard v2, updating to PHPUnit 9.1, potentially adding psalm or phpstan to the
CI matrix, performing deprecations, porting tooling to laminas-cli, adding
new CLI commands, and, most importantly, triaging and resolving all open issues.

There was some back-and-forth around the benefits of psalm or phpstan in the CI
matrix, as well as which we should target (though we were heavily leaning
towards psalm).

In the end:

- We decided to move the discussion of psalm vs phpstan and how to integrate
  them to another time, as it affects more than just Mezzio.
- We voted to proceed with the rest of the proposed work; Matthew and/or Michał
  will create an organization-level project to track the items.

## laminas-cache

Max has created two new packages, laminas-cache-storage-adapter-template and
laminas-cache-storage-adapter-test, as the first steps towards splitting the
various storage adapters into discrete packages. He asked if we can move these
into the Laminas organization and get packages created on Packagist. His main
concern is when to make them public.

The consensus is: we can make them public any time, and issue 0.X releases until
the API is stable. This allows others to see that activity is happening, so that
they can provide review or testing.

Since this was around work we'd already agreed to do, no vote was held. Matthew
will help Max bring the repos into Laminas, as well as register packages on
Packagist.

## Release Cadence

We decided not to discuss this at this time; we can discuss it once we're seeing
more activity and have a better idea of how often releases are being made, and
how quickly we are triaging and resolving issues and patches. The hope is that
with the new workflow, and more attention from TSC members, cadence will not be
an issue.
