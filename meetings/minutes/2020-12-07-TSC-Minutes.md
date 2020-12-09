# Minutes from the 2020-11-02 Laminas Technical Steering Committee Meeting

- When: 2020-12-07 at 19:00 UTC, until 20:26 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Aleksei Khudiakov
  - Frank Brückner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Max Bösing
  - Matthew Weier O'Phinney
  - Michał Bundyra

Quorum was met (8 out of 15 members were present).

## Agenda

-  Pull request instructions are out of date, referring to master and develop branches which do not exist any more. ([jump to discussion](#pull-request-instructions))

## Pull Request Instructions

A contributor noted that the `CONTRIBUTING.md` is out-of-date, and Matthew noted that the proposed maintainers guide was not yet complete, either.

The main topic holding up changes was around the topic of merges, and whether or not we should standardize on one over another.

We noted that all three styles (normal merge, squash and merge, and rebase and merge) have been used, and each has pros and cons:

- Normal merges add an additional merge commit.
  They can often make the history visualization more complicated.
  But they also make it easy to revert an entire change at once, and they retain the full history that led to the change.
  This latter is a double-edged sword, however, as a given patch might have a lot of small, unannotated commits.

- Squash and merge simplifies the history, particularly when a lot of little, unannotated commits are made.
  The resulting squashed commit gives us a single artifact representing (ideally) a single change, which can make reading the history easier.
  However, this also means that it's difficult to do a granular reversion (e.g, when only one change out of many needs to be reverted).
  And a lot of history, including the decisions that led to a change, can get lost.
  Finally if a user was tracking the branch and building additional patches off of it, they are forced to rebase and/or cherry-pick in order to make their own branch mergeable.

- Rebase and merge makes for a linear history, and keeps all history leading to a change.
  However, it suffers from the last problem presented for "squash and merge" in that the rebase operation changes commit identifiers, which can make derivative patches conflict.
  Additionally, if a lot of small patches are made, we can be left with many small, unannotated commits cluttering the history.

We had a lot of back and forth on this. While Matthew has often used rebase and merge, he has also observed the problems with identifiers.
Michał has had good luck in his current company with using squash and merge, but he also is fully aware that many on his team are doing small commits for each experimental change leading to the final change, and thus squash and merge helps simplify the history tremendously.
Marco and Matthew indicated that they use `git rebase -i` judiciously on their own patches to remove extraneous commits, leaving what history that is present useful to keep, and Michał agreed that he'd want to choose between a standard merge and a squash and merge based on the type of commit history present in the patch.
Luís indicated that he, too, likes to do atomic commits, and then use the merge commit as a boundary indicating the complete set of changes for a given patch.

In the end, we decided:

- If the PR has a lot of "garbage" or "noisy" commits, the maintainer can use the squash and merge strategy when merging within the GitHub UI.
- Otherwise, the maintainer should use the standard merge strategy when merging within the GitHub UI.
- When merging from the CLI, the maintainer can choose either a standard merge (`git merge`) or a fast-forward merge (`git merge --ff`) based on personal preference.
- We should try and educate contributors about the usage of `git rebase -i` and `git commit --fixup` + `git rebase --autosquash` for the purposes of creating a clean history for a patch.

## Rebasing Patches To Earlier Branches

As a follow-up to this discussion, Matthew noted that with the default branch of repositories representing the next _feature_ release, we're getting a number of bugfix patches that are now targetting the wrong branch.
Updating the PR to target the earlier branch means that there are now extraneous commits from the newer branch being shown.
His solution so far has been to create a new branch and cherry-pick, but he wondered if there was an easier solution.

Luís and Michał pointed out that you can do `git rebase -i {target branch}`, and drop the commits that you did not create for the patch.
This approach has an added benefit, as the author can then squash related commits together at the same time, cleaning up the history.

## "Master" Branch References and License DocBlocks

From here, Aleksei noted that the license docblocks all still point to the "master" branch of the repository.
Since we removed this branch, it means that the link is incorrect; however, it's also a moving target.
Matthew noted that the nice bit is that GitHub redirects these to the default branch.
However, Marco noted that the docblocks are essentially useless.
Matthew concurred, pointing out that we have LICENSE and COPYRIGHT files in each repository, and since code is installed with these files, it's up to the distributor of code to ensure that attribution is present.
Marco noted that the docblock is a construct from the bad-old-days of "download an archive and apply patch" (pre-Composer, basically).

As such, we have decided to remove the docblocks from code files.

Geert has volunteered to add a rule to the coding standards that will detect them, and a corresponding fixer to remove them.

## GitHub Actions Update

During our [last meeting](2020-11-02-TSC-Minutes.md), we decided to start migrating to GitHub Actions, and an ad-hoc group was created to start developing a proof of concept or guidelines.
Marco indicated no real work happened as the various members all had become busy.
However, he mentined as well that he needs to test stuff on laminas-code, and Travis-CI availability is currently a blocker for him.
As such, he will try a few approaches, and let us know what worked and what did not, as a start towards this migration.

Max shared some ideas he's played with, and also that Ben Ramsey has an action he's used for these purposes that we might be able to build off of.

## Summary

We had a very small agenda, but lots of topics to discuss around QA.
Hopefully we can firm these up in the next month or two, and start advertising for new maintainers for our various repositories.
