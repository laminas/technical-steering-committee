# Next Technical Steering Committee Meeting Agenda

- Date: 2021-01- (TBD; either 04 or 11)
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

### Drop `CHANGELOG.md` from repositories when it leads to merge conflicts

`CHANGELOG.md` is more hindrance than help: we keep our changelog in the `git tag` history, as well
as under the release history on github. Having `CHANGELOG.md` as part of the repository leads to
slower merge-up workflow when dealing with bugfixes, and we already have a all the information in
the repository history, as well as on github.

An alternative suggested approach could be to generate a `CHANGELOG.md` in the documentation build,
by picking the list of pre-existing tags and unrolling it in that process, therefore removing the
need for keeping a build artifact in the repository.

Examples:

 * https://github.com/laminas/laminas-servicemanager/pull/76
 * https://github.com/laminas/laminas-mail/pull/125 merge-up actively interrupted a productive day of merge/release there: https://github.com/laminas/laminas-mail/pull/125#issuecomment-752996771
