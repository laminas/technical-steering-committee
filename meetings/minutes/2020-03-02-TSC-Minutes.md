# Minutes from the 2020-03-02 Laminas Technical Steering Committee Meeting

- When: 2020-03-02 at 21:00 UTC
- Where: Laminas Slack
- Attending:
  - Adam Lundrigan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Michał Bundyra

## Terms

- BC: Backwards Compatibility
- CB: Community Bridge
- EOL: End Of Life
- LF: Linux Foundation
- LTS: Long Term Support
- TBD: To Be Determined
- TSC: Technical Steering Committee
- ZF: Zend Framework

## Agenda

This was the proposed agenda; not all topics were discussed.

- TSC Members - inclusion / exclusion
- Financing
  - Full-time employed Maintainers?
- LTS strategy - Should Laminas provide LTS releases or not?
  - LTS Lifecycle
  - LTS and Dependencies
- Components usage - what is currently relevant, what isn't?
- New components - when? Who has new patterns?
- Migrating existing libraries to laminas: interesting to propose that to the
  community at large?
- PHP Version bump strategy
- MVC Support - Active Development?
- Roadmap for components
- Doctrine integration
- Major release community guideline
  - Breaking change review and approval process
  - Time constraints between major releases
  - What should be considered a minimal change to warrant major release
  - Soft upper time limit for how long major release can be postponed to wait
    for more major targeting features to be completed
  - Overall stance on breaking non-feature changes aimed at improving code and
    design quality. Signature changes, adoption of new language features.
  - Feature deprecation and removal timeframe

## TSC Membership

Membership is governed by the forthcoming charter, and requires a majority of
the TSC to vote for either a new member, or to remove one.

Several ZF community review team members have indicated in the past couple
months that they will no longer have time and/or interest in participating. Some
we haven't heard from, and Matthew will follow up with them in the coming days.

During the meeting, Matthew asked if there are any community members the TSC
members would like to propose join the TSC, and a list of around a half-dozen
was produced. Matthew will follow up with them to determine if they are
interested, and, if so, formally propose them to the TSC as new members.

## Financing Goals

Currently, we are an unfunded technical project with the Linux Foundation, and
are still finalizing our technical charter. While Matthew will be re-starting
funding efforts via corporate memberships, we have options we can pursue before
corporate memberships are in place.

As soon as the TSC charter is approved by the LF, the project can start
accepting donations.  Matthew has already setup a Community Bridge account for
Laminas.  Community Bridge is a tool the LF provides that allows projects:

- the ability to accept one-time donations
- the ability to accept recurring monthly donations
- the ability to create Kickstarter-like campaigns with specific funding goals

During discussions, the various TSC members agreed that the goal should be to
fund a developer either part-time or close to full-time, and set an initial
budget of 36k USD per year. How we get there is still TBD.

One proposal is a Kickstarter-style campaign setting an initial goal of hiring
somebody full-time for X months.

Another proposal is that we setup Patreon-style tiers, if possible, with goals of:

- 3k/month: fund one person
- 5k/month: fund one person, plus a part-time person to work on documentation
- 6k/month: fund two people

Matthew will look into whether or not CB provides Patreon-style tiers, and, if
not, if there are other platforms we might be able to leverage.

### Summary

No decisions made, other than the amounts of funding we will aim for initially.
Matthew will do some more research on what platforms we can use with the LF, and
open up donations via CB once the charter is approved.

## LTS Policy

Matthew opened with a proposal that we do not set an LTS policy at all, and
leave it to commercial entities to provide. His rationale was:

- LTS is logistically difficult for maintainers, and we have lost maintainers
  due to LTS policies in the past.
- Generally, if a company requires LTS, they are willing to pay for it.

Marco countered that we at least need a security policy that provides users with
some peace-of-mind that they don't need to upgrade to a new major version
immediately. He proposed a "Security Window" policy:

- The **currently** maintained release tree always receives security patches.
- A minor release tree receives security backports until the minimum supported
  PHP version it supports has reached an EOL status (as supported by php.net).

Marco suggests a "merge-up" strategy: you target the earliest supported minor
release with the initial patch, and then merge up until you hit the current
release tree.

As an example, let's consider a package where:

- Version 3.0.0 supported PHP 7.0
- Version 3.1.0 supported PHP 7.1
- Version 3.2.0 supported PHP 7.2
- Version 3.3.0 supported PHP 7.3
- Version 3.4.0 supported PHP 7.3
- Version 3.5.0 supported PHP 7.4

Currently, PHP.net has droped support for 7.0 and 7.1. As such, if a security
issue is reported, we would:

- Create a patch against the latest release in the version 3.2 series, and cut a
  new release.
- Merge the patch up to the 3.3 series, and cut a new release.
- Merge the patch up to the 3.4 series, and cut a new release.
- Merge the patch up to the 3.5 series, and cut a new release.

This approach can be automated somewhat with tools such as
doctrine/automatic-releases, and merging up is generally easier and less
error-prone than backporting.

This approach had wide-support among the TSC members, as (a) it is easy to
message, and (b) leads to quicker adoption of new PHP releases. As a bonus, it
means that we get to start fresh with the majority of our components, as most of
them pin to 5.6 or 7.1 on the lower version boundary.

As such, the discussion quickly moved to the next topic, PHP Version Adoption
Strategy.

### Summary

- We will adopt a Security Window policy.
- Current release branches (generally the `master` branch of a given repo) will
  receive security patches directly.
- A given minor release branch will continue to receive security backports until
  the minimum PHP version it supports is no longer supported by php.net.

## PHP Version Adoption Strategy

We have had off-and-on discussions on this topic for several years. Matthew's
policy had always been to only bump the minimum supported PHP version on a new
_major_ release. Marco, however, has been pushing for Doctrine's strategy, which
is to bump the minimum PHP version constraint at minor version releases.

One huge benefit of this latter approach is that it ties well into a security
window policy, and even encourages bumping versions as quickly as possible in
order to reduce the number of versions of a given package we need to support at
any one time.

Those in the meeting noted that bumping the minimum supported version does not
necessarily mean adopting that version's language features. However, it does
open the door to refactoring code to use those features, so long as they do not
break the public API (e.g., we cannot start using typehints in parameters that
did not previously have them, etc.).

Marco also proposed that we consider adopting a strategy of pinning a given
release to a specific PHP minor version (e.g., using the `~7.4.0` semantics); we
decided to table a decision on that to a later date.

### Summary

- We will immediately allow bumping the minimum supported PHP version in new
  minor releases.
- At a later date, we will consider whether or not to pin minor releases to
  specific PHP minor releases.

## Community Guidelines Around Major Releases

Leading directly from the LTS Policy and PHP Version Adoption Strategy
discussions, we jumped into major release guidelines for maintainers.

The consensus is that we do pretty much as we have been since the 2.5 release:

- No set timelines for new major releases. Let them evolve as they need to.
- Major releases should be done primarily when:
  - A BC break cannot be avoided.
  - There are good tradeoffs (e.g., code maintainability, API simplification)
    for creating a BC break.

Additionally, we decided that:

- New major releases require TSC approval.
- Any plan to introduce a new major version SHOULD include a transition plan,
  which can include any of:
  - A transitional release providing forwards-compatibility features.
  - Tooling to help users migrate.
- Maintainers MUST request a TSC review before merging a BC-breaking change.
  This is done to ensure that BC breaks are not merged that we would not have
  approved normally.

### Summary

Business as usual, with the exception that maintainers must ask for permission
from the TSC before merging BC-breaking changes, or if they want to propose a new major
version.

## Migrating existing libraries to Laminas

Matthew misinterpreted this topic to mean "helping other OSS projects that
currently consume ZF to migrate to Laminas," and indicated he has an action item
already to identify projects and contact their developers.

Marco, however, provided the agenda item and clarified it to mean: "will we
allow bringing in libraries from other sources?" As an example, Michał has
developed a library for providing a `laminas` CLI tool that components can hook
into; would we allow bringing it into Laminas in the future?

We all agreed that this is something we support, with the following workflow:

- Users develop the library elsewhere (e.g., under their own username on
  GitHub), optimally using their own namespace (in case we choose not to adopt
  it).
- A TSC sponsor is required to propose that we adopt the library.
- A TSC vote is required for accepting it.
- The TSC sponsor and the author are the initial maintainers.

The discussion then moved to: how does an author bring a library to the TSC's
attention in order to get a sponsor? Aleksei proposed we use a custom issue
template on the TSC repository for proposing a library to Laminas. Marco agreed
to create this, and Matthew agreed to put a page on the getlaminas.org website
around the workflow.

### Summary

We definitely want to add new libraries, so long as they have general use cases.
New libraries require a TSC sponsor and a vote before inclusion.

## Conclusion

At this point, we were two hours into the meeting. We do not expect TSC meetings
to run this long in the future, but as the inaugural meeting, we had a lot of
material to cover! We will hold meetings monthly, and Matthew will start
gathering availability from TSC members during the last week of the month.
