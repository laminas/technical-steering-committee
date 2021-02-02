# Minutes from the 2021-02-01 Laminas Technical Steering Committee Meeting

- When: 2021-02-01 at 19:00 UTC, until 20:23 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl (left before DCO discussion)
  - Frank Brückner
  - Geert Eltink
  - James Titcumb (left before laminas-servicemanager vote)
  - Marco Pivetta
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra
  - Rob Allen

Quorum was met (12 out of 15 members were present).

## Agenda

### Drop `CHANGELOG.md` from repositories when it leads to merge conflicts

([jump to discussion](#dropping-the-changelog-md))

[Marco](https://github.com/ocramius) suggests that `CHANGELOG.md` is more hindrance than help: we keep our changelog in the `git tag` history, as well as under the release history on github.
Having `CHANGELOG.md` as part of the repository leads to slower merge-up workflow when dealing with bugfixes, and we already have a all the information in the repository history, as well as on github.

An alternative suggested approach could be to generate a `CHANGELOG.md` in the documentation build, by picking the list of pre-existing tags and unrolling it in that process, therefore removing the need for keeping a build artifact in the repository.

Examples:

- https://github.com/laminas/laminas-servicemanager/pull/76
- https://github.com/laminas/laminas-mail/pull/125 merge-up actively interrupted a productive day of merge/release there: https://github.com/laminas/laminas-mail/pull/125#issuecomment-752996771

### Future of laminas-servicemanager 4.0

([jump to discussion](#future-of-laminas-servicemanager))

[Max](https://github.com/boesing) wants to talk about the next step with `laminas-servicemanager` v4.

As we had huge problems with `laminas-servicemanager` `3.5.0` which had to be fully reverted due to the versioning problem when `laminas-automatic-releases` was added.

Since then, Max backported all potential non-breaking changes from the real `4.0.x` branch to `3.6.x` which already received 3 patches (2021-01-25) regarding BC breaks which were not covered by unit tests.

So as of now, `3.6.x` and `4.0.x` are quite derived. Thus said, there are several fixes in `3.6.x` which should find their way back to `4.0.x` but merging up all these changes would end up in a huge mess.

The only breaking change in the `4.0.x` branch should be the `PSR-11` changes of all interfaces (**assumption**). [Matthew](https://github.com/weierophinney) also created an [RFC](https://discourse.laminas.dev/t/rfc-removal-of-container-interop-from-laminas-servicemanager/1608) regarding `PSR-11` which did not yet had a huge audience. So Max is calling changes in `4.0.x` as obsolete and thus suggests to drop `4.0.x` until we have a proper migration strategy.

### Drop DCO requirement

([jump to discussion](#dropping-commit-based-dco))

From [Stackoverflow](https://stackoverflow.com/questions/1962094/what-is-the-sign-off-feature-in-git-for) (not authoritative, but good source), it seems clear that DCO requirements come from a silly lawsuit that never actually got pushed through.
Requiring DCO has been a constant pain, and I (@ocramius) have been regularly ignoring/skipping it myself too for many patches for which chasing down the author is just irrespectful of both maintainer and contributor time.

We already do regular signed git releases that certify authenticity of our code, and we are well aware that we cannot copy-paste code from proprietary components, and that is already part of our review process.

[Matthew](https://github.com/weierophinney) notes that this was a requirement for being a part of the Linux Foundation, and that:

- Commits made from the GitHub web UI can include the verbiage `Signed-Off-By: {fullname}<{email}>` to fulfill the DCO bot requirements.
- Maintainers have the option of marking the DCO check as passing.

However, these do not solve the problems of users who are not aware of the DCO requirement when doing a UI-based commit, those unfamiliar/uncomfortable with git tooling to add sign-off via rebase, and/or those uncomfortable having their email address in the commit message itself (as GitHub will use an obscured email for those who choose to keep their email private).

[Maks3w](https://github.com/Maks3w) suggests an alternate integration that allows performing DCO sign-off via a GitHub comment (specifically [this one](https://github.com/cla-assistant/github-action), and Matthew has contacted our LF legal counsel to determine if this is viable.

### Adopt the proposed GitHub Actions workflow

([jump to discussion](#github-actions))

[Matthew](https://github.com/weierophinney) worked on a variety of GitHub Action workflows for implementing CI tooling, due to the fact that we used up our Travis-CI minutes yet again by mid-month.
The work he has done was based in part by reviewing workflows on other projects, some experimentation with how matrix settings work, and reviewing work [Marco](https://github.com/ocramius) did on the laminas/laminas-code repository.
He has now provided an [RFC on how to implement our workflows](https://github.com/laminas/technical-steering-committee/issues/61), and would like to get approval to start rolling it out.

## GitHub Actions

As part of his work on the RFC, [Matthew](https://github.com/weierophinney) had written a [PR on laminas-eventmanager](https://github.com/laminas/laminas-eventmanager/pull/15) as a proof-of-concept.
Just prior to the meeting, [Marco](https://github.com/Ocramius) had provided some feedback that was going to prompt a slight change in direction.

The two had investigated, and found that:

- GitHub Apps seem ideal, as we can enable them for an entire organization.
  However, they require we host our own runners, which means we'd have to spin up infrastructure of our own, which is precisely what we do not want to do.
- Actions provide a way to encapsulate re-usable functionality, but...
- Workflows are what call on actions themselves.

The idea is to do the following:

- Have a workflow with as little boilerplate as possible.
- Have an action that snoops through the package to determine which PHP versions to run against, which dependency sets to use, and which checks to run.
- Have either a standard set of workflow steps or an individual action that can perform the check(s) indicated.

Marco's idea is to have the step that determines what to run, and what against, do so based on the presence of known configuration files (such as `phpunit.xml.dist`, `phpcs.xml.dist`, `psalm.xml.dist`, etc.), and align that either with composer scripts or specific vendor commands.

Marco would prefer if we could have a single action that both creates the matrix and runs the tests.
However, [Cees-Jan](https://github.com/WyriHaximus) and Matthew indicate that this isn't really possible in current iterations of GHA; we would need to have one for creating the variables for the matrices, and another for running them.

At this point, we agreed on the approach, and Matthew, Marco, and Cees-Jan agreed to meet later in the week to do a spike and try and get an MVP ready to test.

## Dropping the CHANGELOG.md

[Matthew](https://github.com/weierophinney) noted that he was initially against this, but that after a discussion with [Marco](https://github.com/Ocramius), the two came to the conclusion that IF we need keep-a-changelog style notes (which we often DO), we can push them into the milestone description, as we already pull from it.

As such, his reservations about removing it are gone, and his only suggestion is to potentially push an initial empty changelog template _into_ the milestone description when creating it from the automatic-releases workflow.
[Geert](https://github.com/geerteltink) and [Andreas](https://github.com/heiglandreas) asked for a clarification of what Matthew meant by adding an empty changelog; Matthew indicated the various "Added", "Removed", etc. sections from the Keep A Changelog format.
There was also some confusion on where release notes would be available, to which the answer was:

- Pre-release, they would be in the milestone description, and based on any issues/patches assigned to the milestone.
  Maintainers would be able to edit them by clicking the milestone from an issue or patch page, then clicking the "Edit Milestone" button.
- After release, the notes would be in the GitHub release, as well as the tag message.

Since the automatic-releases tooling already consumes the milestone description to create the release notes and tag, nothing needs to change immediately other than removing the `CHANGELOG.md` file.

We did identify a couple of potential process changes we could accommodate in the future, however:

- Adding the default contents when creating new milestones via automatic-releases, as noted earlier.
- Adding a `CHANGELOG.md` file to releases that simply contains a link to the new release on GitHub (requires changes to automatic-releases).
- Potentially appending the body of the commit message from the merge commit as additional contents for the milestone description (this would require an additional GHA workflow).

We did a vote, which passed unanimously.
We will start removing `CHANGELOG.md` files from packages, and calling out user-facing changes via the milestone description going forward.

## Future of laminas-servicemanager

[Max](https://github.com/boesing) has been working on moving [laminas-servicemanager](https://github.com/laminas/laminas-servicemanager) forward.
He notes that when we moved to release branches, whoever did so accidentally made the master branch into the 4.0.x branch, and the develop branch into 3.5.x.
He untangled that before the 3.6.0 release, and backported some of the changes from the 4.0.x branch into the new release, but this has made the 4.0.x branch almost impossible to up-merge to.
His question is whether we should drop the 4.0.x branch and re-create it from the 3.6.x branch, and/or whether or not to even work on a 4.0 series yet.

[Matthew](https://github.com/weierophinney) immediately jumped in with a vote to drop the 4.0.x branch and restart it, and noted that the main driver for 4.0 is to drop support for container-interop (the precursor to PSR-11) in favor of PSR-11.
Max noted that this was his understanding as well, but he's unsure what the upgrade path would be for end-users.
Matthew notes that we definitely need either tooling to help post-migration or some sort of forwards-compatible release in the 3.x series; past initiatives, such as the ZF3 push, proved that these helped us retain users.

At this point, [Marco](https://github.com/Ocramius) suggested we write a [rector](https://getrector.org/) for the upgrade, and tagged [Abdul](https://github.com/samsonasik), as he now works there.
Abdul agreed this would be relatively straight-forward, and we could likely even expose any such rector(s) written via our own CLI tooling.

We voted at this point, and the vote was unanimously in favor.
We will drop the existing 4.0.x branch, recreate it from the current 3.6.x branch, and start the work of cutting over to PSR-11 in it.
Abdul will work with Max to create a rector end-users can use to rewrite their own factories, abstract factories, plugin managers, etc. to target PSR-11 instead of container-interop interfaces.

## Dropping commit-based DCO

[Marco](https://github.com/Ocramius) wrote up a nice summary (in the agenda, above).
Since then, [Matthew](https://github.com/weierophinney) reached out to our LF reps, and it sounds like the idea of putting the DCO sign-off in a comment is _already supported_.
So we just need to test it out.
The user just needs to add a comment with `Signed-Off-By: {email}`, and use the same email that is associated with their commits.

Marco felt that if this works, it solves the contribution issues he's been seeing.
If it doesn't, it sounds like the Linux Foundation is okay with us either implementing something like this, or requesting the authors of the DCO bot to implement it.
Either way, we have a path forward, and no decision is required at this time.

## Summary

This was a short and immensely productive meeting, focused largely on helping enable our contributors and maintainers.

Next meeting will be 2021-03-01 at 19:00 UTC in the #tsc-meeting channel of the Laminas Slack.
