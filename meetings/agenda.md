# Next Technical Steering Committee Meeting Agenda

- Date: 2026-05-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Clarification of Vote Requirement for Major Releases _(By @gsteel)_

In the past, I have brought major releases for any subproject to the TSC for a vote prior to tagging;

This gives everyone the chance to request additions/changes, but it is not listed as a requirement in the TSC docs under [decisions requiring a vote](https://github.com/laminas/technical-steering-committee/blob/f0d0bea59e708b655f85e8ede7eaf7d726c991ba/processes/VOTING.md#decisions-requiring-a-vote).

We should document the outcome of this discussion either way by adding it to the list, or adding new sections such as _"Decisions that would benefit from a vote"_, and/or _"Decisions that do not require a vote"_.

### Clean up the Member List

The member list contains a lot of entries that are not active anymore.
We should remove them to keep the list clean and up to date.
This would also free up space for new nominations.

### Speed up the release of ServiceManager v4 support in downstream packages _(By @arhimede)_

Full support for **ServiceManager v4** in Laminas packages has been delayed for almost 3 years.
I worry that many devs, decision makers like CTOs and Head of Engineering who use the packages may lose confidence in the Laminas ecosystem or find alternate solutions.

I agree that the migration process is complex and also that it's temptating to refactor the package at its core, even while battling a lack of time and resources.
The goal is definitely ambitious and commendable, but I feel we need a solution for SM4 alone - sooner, rather than later.
And only then focus on improving the packages at their core.

[Status of v4.0.0 support in laminas components](https://github.com/laminas/laminas-servicemanager/issues/216)

For instance, the work on V3 of `laminas-session` was started in March 2025, and for `laminas-inputfilter` on January 2025.
The current state of things prevents the use of SM4 (and consequently `psr/container` v2) in any current or new projects that use Laminas components.
Also, the more work is being done on the core functionality of a package, the more time and effort will be required to migrate/update production projects.

I am proposing an upgrade procedure in 2 steps for the _in-progress_ packages and the remaining one (`laminas-form`).
Instead of focusing on _v3_, we should split focus into _v3_ and _v4_.

#### Example: `laminas-session` case

`laminas-session` is currently live with version 2.x that has:

- SM3
- Older code
- Older architecture.

The v3 release has these milestones:

- SM4 implementation
- Remove obsolete dependencies (optimize composer)
- Remove old code
- Full refactor
- Major API change
- Rewrite v3 documentation
- Release v2 with mentions of deprecations, backward incompatibilities, API signature changes

But 14 months later and it's still in an `almost-ready` state which is a blocker for certain projects.

#### Proposal

These 1st-level changes should be prioritized:

- Fast lane release for `v3.x`
- Include only minimal, pivotal changes: SM4, upgrade composer dependencies, minimal API changes
- Release v2 with deprecations etc.

Then the focus can fully shift to 2nd-level changes:

- Working on `v4.x` (e.g. core, BC-breaking changes now ready in input-filter v3)
- Slow lane release over the following months for anything not included in the 1st level

The benefits of reducing the scope would be:

- Easier upgrade/refactor from v2 to v3 for package maintainers
- Faster release of SM4 support
- Less effort to upgrade live projects
- Maintaining the public interest in the Laminas ecosystem


