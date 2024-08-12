# Minutes from the 2024-07-01 Laminas Technical Steering Committee Meeting

- When: 2024-08-12 at 19:00 UTC, until 20:16 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Frank Brückner
  - George Steel
  - James Titcumb
  - Julian Somesan
  - Marco Pivetta
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Max Bösing
  - Rob Allen

Quorum WAS met (10 out of 16 members were present).

## Agenda

### Abandon `mezzio/mezzio-aurarouter`

As per [the RFC](https://github.com/mezzio/mezzio-aurarouter/issues/12), should we abandon this package and archive it?

#### Discussion

General agreement that we should abandon it.
It's not got a lot of installs, the upstream library is not getting active maintenance, and the point of having a router abstraction is to allow folks to build their own around other libraries if they want to.

#### Decision

After we reached quorum, we held a vote, which was unanimously in favor.
We will abandon the package.

George will do the honors.

### Maintenance Chores

#### Old Release Branch Clean Up

Packages like `laminas-validator` have a _lot_ of branches. Many of these branches will never see any more commits, and it is trivial to re-create those branches if we ever need to add a patch to an old release.

Is it acceptable to delete release branches older than say 1 year?

##### Discussion

George pointed out that the [PR proposing the topic](https://github.com/laminas/technical-steering-committee/pull/187) has some comments that indicate we can likely delete any branch where the minimum supported PHP version is no longer supported, as those branches will not get any further releases.

Rob asked if there were any benefits to doing this.
Matthew W pointed out that it makes it easier to identify which branches can still get releases.
Rob asked if this was a problem; Matthew and George pointed out that laminas-validator has a LOT of branches at this point, so, yes.

Rob then asked if it was automatable.
Matthew pointed out it likely is, but will take somebody taking the time to do so.

George indicated that he may go ahead and do it manually.

#### Old Milestone Clean Up

Similar to the above, deleting _(not closing 😂)_ old patch milestones. Acceptable?

##### Discussion

General agreement on this as well, as long as the milestone cannot be released to accommodate a security patch.
Marco indicated he had wanted to script this stuff, but never got around to it.

### Laminas Validator v3 Release

Myself _([@gsteel](https://github.com/gsteel))_ and Frank _([@froschdesign](https://github.com/froschdesign))_ have done a lot of work to [`laminas-validator`](https://github.com/laminas/laminas-validator/milestone/5?closed=1) and it is very nearly ready for a v3 release.

Is there anything the TSC wants to see included/changed before we hit the release button?

#### Discussion

Matthew asked what the changes are, and if there is a migration guide.
George answered that the main pieces are:

- Removal of `set*()` methods; all dependencies MUST be passed to constructors now.
- All validators are now marked `final`.
- Update to laminas-servicemanager v4.
- Improvements to the code that bring the Psalm baseline down to almost nothing.
- Documentation improvements.

The migration guide is already in place, and deprecations were already created in a v2 release.

#### Decision

We held a vote, and unanimously agreed to the v3 release.

### New maintainers

Julian proposed two new maintainers from his DotKernel team, [Claudiu](https://github.com/cPintiuta) and [Alex](https://github.com/alexmerlin).

#### Discussion

The main discussion was around (a) if either have a history of PRs we can use as a reference, and (b) if there are specific repositories proposed for maintenance.
Rob even suggested it would be useful to see at least 2 PRs merged from folks who want to be maintainers, as they will have been through the process and have an idea what we look for.

Each has only had one PR merged, and only Claudiu has a specific repo proposed (laminas-filter).

Matthew suggested we have them do additional PRs this month, and flag the TSC for review, as well as have them do some PR reviews.
This work will allow us to see how they interact with others, and give them some guidance before we vote to give them maintainer rights.
Rob agreed, and suggested that comments on issues and PRs are ideal, as they are a large part of a maintainer's role.

#### Decision

We will vote on these maintainers next month, after having them submit some more PRs as well as do some code reviews.
