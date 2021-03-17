# Laminas Project Maintainers

We aim to have 2+ maintainers per repository.
Maintainers have GitHub maintainer rights to the repository(ies) they maintain, which means the ability to push code to the repository, manage issues and pull requests, and manipulate selected repository settings.

To become a maintainer, you must first have another maintainer or a TSC member nominate you to the TSC.
Nominations are done by submitting an issue to this repository with a title prefix of `[NOMINATION][MAINTAINER]` (or select the "Maintainer Nomination" issue type when creating an issue on this repository).
Maintainers are approved by a majority vote of the TSC, which will be held no later than 1 week following the nomination.

Current maintainers are found on the Teams page of each organization, on a team matching the repository name:

- [Laminas organization teams](https://github.com/orgs/laminas/teams)
- [Laminas API Tools organization teams](https://github.com/orgs/laminas-api-tools/teams)
- [Mezzio organization teams](https://github.com/orgs/mezzio/teams)

## Maintainers Guide

This guide is intended for *maintainers* — anybody with commit access to one or more Laminas Project repositories.

We use [automatic-releases](https://github.com/laminas/automatic-releases) for managing the various Laminas Project repositories.
At a glance, this means:

- Releases are defined by milestones in GitHub.
- The milestone **MUST** be named by a specific semantic version number with major, minor and patch number, without a prefix (example: `1.0.0`).
- There **MUST** be a release branch matching the minor version of this milestone.
- These release branches **MUST** be named by major and minor version numbers and a literal `x` for the patch number, without a prefix (example: `1.0.x`).
- When such a milestone is closed, the automatic-releases workflow will perform the following actions:
  - Create a tag named by the version number.
  - Create a new release via the GitHub API.
  - If a release branch exists for the next *minor* version of this milestone, it will create a PR with the released changes against this branch.
  - If there is no release branch for the next *minor* version of this milestone, it will be created.
- All pull requests **MUST** be assigned to a milestone that matches the release branch.
- Pull requests that are adding new features **MUST** target the most recent, unreleased branch.
- Pull requests with bugfixes may target any actively maintained release branch.
- A release branch can continue to receive patches only as long as the lowest supported PHP version is still supported by php.net, or if it is the latest available release branch.
  As an example, if today is 2020-12-09, and the minimum supported PHP version for a release branch is 5.6, and a newer release branch exists, then the branch is no longer supported.

Maintainers can choose to release new maintenance releases with each new patch, or accumulate patches until a significant number of changes are in place.
Security fixes, however, must be coordinated with the TSC to ensure an advisory is made, a CVE is created and the fix is applied to all releases within the current security support window.

## Reviewing Pull Requests

We recommend reviewing pull requests directly within GitHub.
This allows a public commentary on changes, providing transparency for all users.

When providing feedback be civil, courteous, and kind.
Disagreement is fine, so long as the discourse is carried out politely.
If we see a record of uncivil or abusive comments, we will revoke your commit privileges and invite you to leave the project.

During your review, consider the following points:

- Does the change have impact?
  While fixing typos is nice as it adds to the overall quality of the project, merging a typo fix at a time can be a waste of effort.
  (Merging many typo fixes because somebody reviewed the entire component, however, *is* useful!)
  Other examples to be wary of:

  - Changes in variable names.
    Ask whether or not the change will make understanding the code easier, or if it could simply a personal preference on the part of the author.

  - Formatting changes.
    Most formatting changes should be generated only by a coding standards checker/fixer — and those will normally be caught by continuous integration.
    Ask whether the change is generally improving readability/maintenance, or if it could simply be a personal preference on the part of the author.

  Essentially: feel free to close issues that do not have impact.

- Do the changes make sense?
  If you do not understand what the changes are or what they accomplish, ask the author for clarification.
  Ask the author to add comments and/or clarify test case names to make the intentions clear.

  At times, such clarification will reveal that the author may not be using the code correctly, or is unaware of features that accommodate their needs.
  If you feel this is the case, work up a code sample that would address the issue for them, and feel free to close the issue once they confirm.

- Does the change break backwards compatibility (BC)?
  If so, work with the contributor to determine why the BC break is needed, and whether or not there may be a way to make the change without breaking BC.
  Breaking BC should be done only out of necessity, and any break should have accompanying documentation on the impact, as well as how to update applications to accommodate the changes.

  If at all possible, try and introduce new behavior and deprecate existing behavior.
  This allows users to gradually migrate over a period of releases.
  The existing, deprecated behavior can then be removed in a later major release.

  Any BC breaks you plan on merging MUST be communicated to the [Laminas Technical Steering Committee](https://github.com/laminas/technical-steering-committee) to ensure that testing can be done on related components.

- Is this PR fixing a bug?
  If so:

  - Make sure the PR is targeting a previous release branch.
    Most likely a contributor will open the PR against the current release branch, which is targeting a future minor release.
    When this is the case, re-target the PR against the previous release branch and guide the contributor to rebase/cherry-pick their changes.

- Is this a new feature?
  If so:

  - Does the issue contain narrative indicating the need for the feature?
    If not, ask them to provide that information. Since the issue will be linked in the changelog, this will often be a user's first introduction to it.

  - Are new unit tests in place that test all new behaviors introduced?
    If not, **do not merge** the feature until they are!

  - Is documentation in place for the new feature?
    (See the [documentation guidelines](https://github.com/laminas/documentation/blob/master/CONTRIBUTING.md)).
    If not **do not merge** the feature until it is!

  - Is the feature necessary for general use cases?
    Try and keep the scope of any given component narrow.
    If a proposed feature does not fit that scope, recommend to the user that they maintain the feature on their own, and close the request.
    You may also recommend that they see if the feature gains traction amongst other users, and suggest they re-submit when they can show such support.

  - Is the feature BC compatible?
    If so, there's nothing blocking merging it, so long as it passes review, and you can tag it for the next minor release.
    If it's not, however, you have a decision to make: will the next version be a minor, or a major release?
    If you decide that you are not ready for a major release yet, indicate to the author that you are not yet ready to merge, and ask them to please keep the patch up-to-date with any merged changes so that it's mergeable when you are ready to schedule a new major release.

    This workflow ensures that the author of the patch is responsible for any merge conflicts.
    Since the author is the one most familiar with the changes they are introducing, they are the party most likely to resolve conflicts correctly.

## Workflow for merging Pull Requests

Pull Requests should only be merged into the correct release branches:

- If the PR is a bugfix, it should target one of the previous release branches, usually the one immediately preceding the current default branch.
  The only exception is when the package is not yet released and therefore has only one release branch.
- If the PR is a new feature, merge it to the latest release branch **only**.

You can merge it by using the green "Merge" button in github.
Generally, speaking, you should choose the option "Create a merge commit".
If the PR contains a lot of small, undocumented changes (e.g., many small changes to incorporate feedback, or small fixes to correct testing, CS, or other errors), you can choose the "Squash and merge" option.
(We do not recommend using "Rebase and merge", as it can potentially break scenarios where multiple patches are created off of each other; in such cases, the commits have differing hash identifiers, which can make keeping the later patches up-to-date difficult.)

Alternatively you may clone the repository and merge the PR locally.
If you decide to do so, do not apply additional changes to the merge.
When merging, you have the option of using either a normal merge (`git merge`) or a fast-forward merge (`git merge --ff`); the latter, if git allows it, has the benefit of keeping the history more linear.

## Maintaining the Changelog

We follow [Keep a CHANGELOG](https://keepachangelog.com/) when documenting user-facing changes in a milestone.

The format is as follows:

```markdown
### Added

- Adds support for PHP 8.0

### Changed

- Did a change that has user impact. . .

### Deprecated

- Marked such-and-such feature as deprecated; use this-and-that feature to be forwards compatible.

### Removed

- Removed support for PHP versions prior to 7.3.

### Fixed

- A fix for such-and-such could lead to differences in calculations.
```

User-facing changes should be catalogued in the milestone description using the above format, using as many of the sections as make sense for the release.
When the automatic-releases workflow triggers, they will be included in the tag commit message, and the release notes.

Examples of scenarios where notes should be added:

- When a new feature is created.
  Give a short description of what it does, and link to where the documentation will live once released.

- When a change has been introduced that could change behavior.
  Generally speaking, these should only happen during major versions, and are indicative of a backwards compatibility break.
  As such, you should detail what changes the user should make to retain prior behavior, if possible.
  Link to migration documentation, when available.

- Whenever a deprecation is introduced, detail it here, and indicate what alternatives exist, and/or when the functionality will be removed entirely.

- Removals of functionality (BC break!), or removal of support for specific dependency versions (e.g., when bumping the minimum-supported PHP version, or bumping the minimum-supported version of a dependency).

- Generally speaking, only note fixes (the "Fixed" section) if they have user impact — but **always** when the release addresses a reported security vulnerability.

> ### What if a CHANGELOG.md file exists?
>
> If a `CHANGELOG.md` file exists in the repository, you can remove it prior to the next release, and move any entries it contains for the next version into the milestone description for that version.

## Performing a Release

Releases are automatically performed by closing a milestone.
**DO NOT** close the milestone without first closing all related issues and pull requests.
The [automatic-releases workflow](https://github.com/laminas/automatic-releases) will fail in that scenario, and you will need to re-opend and re-close the milestone in order to create the release.

The automatic-releases workflow:

- Gathers release notes from the milestone description and any closed issues or pull requests related to the associated milestone.
- Tags the release, using the release notes, and pushes it to the repository.
- Creates a release in the repository based on the tag, and using the release notes.
- Bumps to the next bugfix version in the changelog, and pushes it to the repository.
- Creates the next minor release branch, if it doesn't already exist, bumping the changelog to the next minor version.
- If the next minor release branch exists, it creates a "merge-up" pull request, with changes since the last bugfix release.
- Creates the next bugfix, minor, and major milestones, if they do not yet exist.

## FAQ

### What if I want to merge a patch made against the default release branch to an earlier release branch?

Occasionally a contributor will issue a patch against the default release branch that would be better suited for an earlier release branch; typically these are bugfixes that do not introduce any new features.
When this happens, you need to alter the workflow slightly.

If you use the [GitHub CLI command](https://cli.github.com):

```console
$ gh pr checkout {PR ID}
$ git rebase -i {target release branch}
# resolve any merge conflicts
$ git push -f
```

And then go edit the PR within Github to change the base branch the PR was open onto.

### What if I want to merge a patch made against an earlier release branch to a later one?

Go for it.

The release branch strategy we use should allow merging without issues; if there are any resolve the conflicts.
