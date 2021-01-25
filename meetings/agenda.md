# Next Technical Steering Committee Meeting Agenda

- Date: 2021-02-01
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

### Drop `CHANGELOG.md` from repositories when it leads to merge conflicts

[Marco](https://github.com/ocramius) suggests that `CHANGELOG.md` is more hindrance than help: we keep our changelog in the `git tag` history, as well as under the release history on github.
Having `CHANGELOG.md` as part of the repository leads to slower merge-up workflow when dealing with bugfixes, and we already have a all the information in the repository history, as well as on github.

An alternative suggested approach could be to generate a `CHANGELOG.md` in the documentation build, by picking the list of pre-existing tags and unrolling it in that process, therefore removing the need for keeping a build artifact in the repository.

Examples:

- https://github.com/laminas/laminas-servicemanager/pull/76
- https://github.com/laminas/laminas-mail/pull/125 merge-up actively interrupted a productive day of merge/release there: https://github.com/laminas/laminas-mail/pull/125#issuecomment-752996771


### Future of laminas-servicemanager 4.0

[Max](https://github.com/boesing) wants to talk about the next step with `laminas-servicemanager` v4.

As we had huge problems with `laminas-servicemanager` `3.5.0` which had to be fully reverted due to the versioning problem when `laminas-automatic-releases` was added.

Since then, Max backported all potential non-breaking changes from the real `4.0.x` branch to `3.6.x` which already received 3 patches (2021-01-25) regarding BC breaks which were not covered by unit tests.

So as of now, `3.6.x` and `4.0.x` are quite derived. Thus said, there are several fixes in `3.6.x` which should find their way back to `4.0.x` but merging up all these changes would end up in a huge mess.

The only breaking change in the `4.0.x` branch should be the `PSR-11` changes of all interfaces (**assumption**). [Matthew](https://github.com/weierophinney) also created an [RFC](https://discourse.laminas.dev/t/rfc-removal-of-container-interop-from-laminas-servicemanager/1608) regarding `PSR-11` which did not yet had a huge audience. So Max is calling changes in `4.0.x` as obsolete and thus suggests to drop `4.0.x` until we have a proper migration strategy.
