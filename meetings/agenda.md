# Next Technical Steering Committee Meeting Agenda

- Date: 2024-08-12
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Abandon `mezzio/mezzio-aurarouter`

As per [the RFC](https://github.com/mezzio/mezzio-aurarouter/issues/12), should we abandon this package and archive it?

### Maintenance Chores

#### Old Release Branch Clean Up

Packages like `laminas-validator` have a _lot_ of branches. Many of these branches will never see any more commits, and it is trivial to re-create those branches if we ever need to add a patch to an old release.

Is it acceptable to delete release branches older than say 1 year?

#### Old Milestone Clean Up

Similar to the above, deleting _(not closing 😂)_ old patch milestones. Acceptable?

### Laminas Validator v3 Release

Myself _([@gsteel](https://github.com/gsteel))_ and Frank _([@froschdesign](https://github.com/froschdesign))_ have done a lot of work to [`laminas-validator`](https://github.com/laminas/laminas-validator/milestone/5?closed=1) and it is very nearly ready for a v3 release.

Is there anything the TSC wants to see included/changed before we hit the release button?
