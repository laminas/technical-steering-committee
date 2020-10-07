# Laminas Project Maintainers

We aim to have 2+ maintainers per repository. Maintainers have GitHub maintainer
rights to the repository(ies) they maintain, which means the ability to push
code to the repository, manage issues and pull requests, and manipulate selected
repository settings.

To become a maintainer, you must first have another maintainer or a TSC member
nominate you to the TSC. Nominations are done by submitting an issue to this
repository with a title prefix of `[MAINTAINER][NOMINATION]`. Maintainers are
approved by a majority vote of the TSC, which will be held no later than 1 week
following the nomination.

Current maintainers are found on the Teams page of each organization, on a team
matching the repository name:

- [Laminas organization teams](https://github.com/orgs/laminas/teams)
- [Laminas API Tools organization teams](https://github.com/orgs/laminas-api-tools/teams)
- [Mezzio organization teams](https://github.com/orgs/mezzio/teams)

# Maintainers Guide

This guide is intended for *maintainers* — anybody with commit access to one or more laminas Framework
repositories.

We use [automatic relases](https://github.com/laminas/automatic-releases) for
managing the various laminas Framework repositories. At a glance, this means:

- releases are defined by milestones in GitHub
- the milestone *must* be named by a specific semantic version number with major, minor and patch number
  without a prefix (example: `1.0.0`)
- there must be a release branch matching the minor version of this milestone
- these release branches *must* be named by major and minor version numbers and a literal `x` for the patch number
  without a prefix (example: `1.0.x`)
- when such a milestone is closed, the automatic-releases workflow will perform the following actions:
  - create a tag named by the version number
  - create a new release via the github api
  - if a release branch exists for the next *minor* version of this milestone, it will create a PR with the released 
    changes against this branch
  - if there is no release branch for the next *minor* version of this milestone, it will be created
- all pull requests *must* be assigned to a milestone that matches the release branch
- pull requests that are adding new features *must* target the most recent, unreleased branch
- pull requests with bugfixes may target any actively maintained release branch.

Maintainers can choose to release new maintenance releases with each new patch, or accumulate
patches until a significant number of changes are in place. Security fixes, however, must be coordinated with 
the TSC to ensure an advisory is made, a CVE is created and the fix is applied to all releases within the current 
security support window.

## Reviewing Pull Requests

We recommend reviewing pull requests directly within GitHub. This allows a public commentary on
changes, providing transparency for all users.

When providing feedback be civil, courteous, and kind. Disagreement is fine, so long as the
discourse is carried out politely. If we see a record of uncivil or abusive comments, we will revoke
your commit privileges and invite you to leave the project.

During your review, consider the following points:

- Does the change have impact? While fixing typos is nice as it adds to the overall quality of the
  project, merging a typo fix at a time can be a waste of effort. (Merging many typo fixes because
  somebody reviewed the entire component, however, *is* useful!) Other examples to be wary of:

  - Changes in variable names. Ask whether or not the change will make understanding the code
    easier, or if it could simply a personal preference on the part of the author.

  - Formatting changes. Most formatting changes should be generated only by a coding standards
    checker/fixer — and those will normally be caught by continuous integration. Ask whether the
    change is generally improving readability/maintenance, or if it could simply be a personal
    preference on the part of the author.

  Essentially: feel free to close issues that do not have impact.

- Do the changes make sense? If you do not understand what the changes are or what they accomplish,
  ask the author for clarification. Ask the author to add comments and/or clarify test case names to
  make the intentions clear.

  At times, such clarification will reveal that the author may not be using the code correctly, or
  is unaware of features that accommodate their needs. If you feel this is the case, work up a code
  sample that would address the issue for them, and feel free to close the issue once they confirm.

- Does the change break backwards compatibility (BC)? If so, work with the contributor to determine
  why the BC break is needed, and whether or not there may be a way to make the change without
  breaking BC. Breaking BC should be done only out of necessity, and any break should have
  accompanying documentation on the impact, as well as how to update applications to accommodate the
  changes.

  If at all possible, try and introduce new behavior and deprecate existing behavior. This allows
  users to gradually migrate over a period of releases. The existing, deprecated behavior can then
  be removed in a later major release.

  Any BC breaks you plan on merging MUST be communicated to the [laminas team](mailto:laminas-devteam@laminas.com)
  and/or [Community Review team](mailto:laminas-crteam@lists.laminas.com) to ensure that testing can be done
  on related components and so that the main laminas release can be tested.

- Is this PR fixing a bug? If so:

  - Make sure the PR is targeting a previous release branch. Most likely a contributor will
    open the PR against the current release branch. When this is the case, re-target the PR
    against the previous release branch and guide the contributor to rebase/cherry-pick their changes.

- Is this a new feature? If so:

  - Does the issue contain narrative indicating the need for the feature? If not, ask them to
    provide that information. Since the issue will be linked in the changelog, this will often be a
    user's first introduction to it.

  - Are new unit tests in place that test all new behaviors introduced? If not, **do not merge** the
    feature until they are!

  - Is documentation in place for the new feature? (See the [documentation
    guidelines](https://github.com/laminasframework/documentation/blob/master/CONTRIBUTING.md)). If
    not **do not merge** the feature until it is!

  - Is the feature necessary for general use cases? Try and keep the scope of any given component
    narrow. If a proposed feature does not fit that scope, recommend to the user that they maintain
    the feature on their own, and close the request. You may also recommend that they see if the
    feature gains traction amongst other users, and suggest they re-submit when they can show such
    support.

  - Is the feature BC compatible? If so, there's nothing blocking merging it, so long as it passes
    review, and you can tag it for the next minor release. If it's not, however, you have a decision
    to make: will the next version be a minor, or a major release? If you decide that you are not
    ready for a major release yet, indicate to the author that you are not yet ready to merge, and
    ask them to please keep the patch up-to-date with any merged changes so that it's mergeable when
    you are ready to schedule a new major release.

    This workflow ensures that the author of the patch is responsible for any merge conflicts. Since
    the author is the one most familiar with the changes they are introducing, they are the party
    most likely to resolve conflicts correctly.

## Workflow for merging Pull Requests

Pull Requests should only be merged into the correct release branches:

- If the PR is a bugfix, it should target one of the previous release branches.
  The only exception is when the package is not yet released and therefore has only 
  one release branch.
- If the PR is a new feature, merge it to the latest release branch **only**.

You may merge it by using the green "Merge" button in github. If you do so, use only the
"Create a merge commit" option. Do **not** use "Squash and merge" or "Rebase and merge". 

Alternatively you may clone the repository and merge the PR locally. If you decide to do so, 
do not apply additional changes other than changelog entries to the merge.

## Maintaining the Changelog

All components follow [Keep a CHANGELOG](http://keepachangelog.com/). This file is merged
with listing of the PRs and issues assigned to milestone of the release. 

The format is as follows:

```markdown
# CHANGELOG

## X.Y.Z - YYYY-MM-DD

### Added

- [#42](https://github.com/organization/project/pull/42) adds documentation!

### Changed

- Nothing.

### Deprecated

- Nothing.

### Removed

- Nothing.

### Fixed

- [#51](https://github.com/organization/project/pull/51) fixes
  Something to be Better.
```

Each version gets a changelog entry in the project's `CHANGELOG.md` file. Not all changes need to be
noted; things like bugfixes, coding standards fixes, continuous integration changes, or typo fixes do not need
to be communicated. However, anything that falls under an addition, deprecation, removal
MUST be noted. Please provide a succinct but *narrative* description for the change you merge.

You may also ask the contributor to add these entries to get a feeling for what they're trying to accomplish.

## Performing a Release

Releases are automatically performed by closing a milestone.

### Tag the milestone

Finally, if a feature is merged to `master`, flag it for the next maintenance milestone (e.g.,
"2.0.4"); if merged only to `develop`, flag it for the next minor or major release milestone (e.g.,
"2.1.0"). This allows users to see when a pull request will release and/or was released.

## Tagging

We recommend tagging frequently. Only allow patches to accumulate if they are not providing
substantive changes (e.g., documentation updates, typo fixes, formatting changes). You *may* allow
features to accumulate in the `develop` branch, particularly if you are planning a major release,
but we encourage tagging frequently.

### Maintenance releases

Tag new maintenance releases against the `master` branch.

First, create a branch for the new version:

```console
$ git checkout -b release/2.5.3
```

Next, update the release date for the new version in the `CHANGELOG.md`, and commit the changes.

Merge the release branch into `master` and tag the release. When you do, slurp in the changelog
entry for the new version into the release message. Be aware that header lines (those starting
with `### `) will need to be reformatted to the alternate markdown header format (a line of `-`
characters following the header, at the same width as the header); this ensures that `git` does
not interpret them as comments.

```console
$ git checkout master
$ git merge --no-ff release/2.5.3
$ git tag -s release-2.5.3
```

> #### Tag names
>
> The various component repositories that were created from the original monolithic laminas2 repository
> use the tag name format `release-X.Y.Z`. This is the format that has been in use by the Zend
> Framework project since inception, and we keep it in these repositories for consistency.
>
> New repositories, such as laminas-diactoros and laminas-stratigility, use simply the semantic version as
> the tag name, without any prefix.
>
> Before you tag, check to see what format the repository uses!

> #### Signed tags are REQUIRED
>
> Always use the `-s` flag when tagging, and make sure you have setup PGP or GPG
> to allow you to create signed tags. Unsigned tags _**will be revoked**_ if
> discovered.

The changelog entry for the above might look like the following:

```markdown
Added
-----

- [#42](https://github.com/organization/project/pull/42) adds documentation!

Changed
-------

- Nothing.

Deprecated
----------

- Nothing.

Removed
-------

- Nothing.

Fixed
-----

- [#51](https://github.com/organization/project/pull/51) fixes
  Something to be Better.
```

You will then merge to `develop`, as you would for a bugfix:

```console
$ git checkout develop
$ git merge --no-ff release/2.5.3
```

Next, you need to create a CHANGELOG stub for the next maintenance version. Use the
`laminas-maintainer changelog-bump` command:

```console
$ path/to/maintainers/bin/laminas-maintainer changelog-bump 2.5.4
```

Spot-check the `CHANGELOG.md` file, and then merge to each of the `master` and `develop` branches:

```console
$ git checkout master
$ git merge --no-ff -m "Bumped version" version/bump
$ git checkout develop
$ git merge --no-ff -m "Bumped master version" version/bump
```

> #### Conflicts
>
> Be aware that this last merge to the `develop` branch will generally result in a conflict, as, if
> you are doing things correctly, you'll have an entry for the next minor or major release in the
> `develop` branch, and you're now merging in a new empty changelog entry for a maintenance release.

Push the two branches and the new tag:

```console
$ git push origin master:master && git push origin develop:develop && git push origin release-2.5.3:release-2.5.3
```

Finally, remove your temporary branches:

```console
$ git branch -d release/2.5.3 version/bump
```

### Feature releases

When you're ready to tag a new minor or major version, you'll follow a similar workflow to tagging a
maintenance release, with a couple of changes.

First, you need to merge the `develop` branch to master:

```console
$ git checkout master
$ git merge develop
```

Assuming you've been following the workflow outlined in this document, this *should* work without
conflicts. If you see conflicts, it's time to read the workflow again!

At this point, you will proceed as you would for a maintenance release, with a
couple changes. In your `versions/X.Y.Z` branch, do the following:

- Check that there is not an empty stub or unreleased maintenance version in the
  `CHANGELOG.md`. For empty stubs, just remove the full entry; for an unreleased
  maintenance version, merge the entries with those for the new minor or major
  release.
- Update the `branch-alias` section of the `composer.json` to bump the
  `dev-master` and `dev-develop` releases. As an example, if you are preparing a
  new `2.8.0` release, `dev-master` would now read `2.8-dev` and `dev-develop` would
  read `2.9-dev`. For a new major version 3.0.0, these would become `3.0-dev`
  and `3.1-dev`, respectively.

After those and any other changes suggested in the "Maintentance releases"
section are made, you can prepare to merge to master and develop. However,
before pushing the branches and tags, do the following:

- Checkout the `develop` branch, and bump the CHANGELOG; use the `--base` argument of the
  `changelog-bump` command to specify the `develop` branch:

  ```console
  $ path/to/maintainers/bin/laminas-maintainer changelog-bump 2.6.0 --base=develop
  ```

- Merge the `version/bump` branch to `develop`.

At that point, you can push the branches, tag, and remove all temporary branches.

## FAQ

### What if I want to merge a patch made against develop to master?

Occasionally a contributor will issue a patch against the `develop` branch that would be better
suited for the `master` branch; typically these are bugfixes that do not introduce any new features.
When this happens, you need to alter the workflow slightly.

- Checkout a branch against develop; use the pull request number, with the suffix `-dev`.

```console
$ git checkout -b hotfix/1234-dev develop
```

- Merge the patch against that branch.

```console
$ git merge <uri of patch>
```

- Checkout another branch against master. Use the pull request number, with no suffix.

```console
$ git checkout -b hotfix/1234 master
```

- Cherry-pick any commits for the patch in the new branch. You can find the sha1 identifiers for
  each patch in the pull request's "Commits" tab.

```console
$ git cherry-pick <sha1>
```

- Merge the new branch to master and develop just as you would for any bugfix.

```console
$ git checkout master
$ git merge hotfix/1234
$ git checkout develop
$ git merge hotfix/1234
```

- Since you did not merge the first branch, `hotfix/1234-dev` in our example, you'll need to use the
  `-D` switch when removing it from your checkout.

```console
$ git branch -d hotfix/1234
$ git branch -D hotfix/1234-dev
```

### What if I want to merge a patch made against master to develop?

Go for it. One reason for choosing `git-flow` is to simplify merges. Because all changes made
against `master` are backported to `develop`, you can safely merge any change issued against the
`master` branch directly to the `develop` branch without issues.

### What order should CHANGELOG entries be in?

CHANGELOG entries should be in reverse chronological order based on release date, and taking into
account *future* release date.

This means that on the `develop` branch, the top entry should always be the one for the version the
`develop` branch is targeting. Additionally, the `develop` branch should contain a stub for the next
version represented by the `master` branch:

```markdown
## 2.6.0 - TBD

### Added

- Nothing.

### Changed

- Nothing.

### Deprecated

- Nothing.

### Removed

- Nothing.

### Fixed

- Nothing.

## 2.5.3 - TBD

### Added

- Nothing.

### Changed

- Nothing.

### Deprecated

- Nothing.

### Removed

- Nothing.

### Fixed

- Nothing.
```

Following this practice ensures that as bugfixes are ported to the `develop` branch, merges *should*
occur without issue, or be untangled relatively easily.

If we decide to skip the maintenance release and go directly to a minor or major release, remove the
stub for the maintenance release when merging the `develop` branch back to `master`. This is best
accomplished by adding the `--no-commit` flag when merging, manually removing the stub from the
changelog and staging it, and then finalizing the commit:

```console
$ git merge --no-commit develop
# edit CHANGELOG.md
$ git add CHANGELOG.md
$ git commit
```

In the case that the `master` branch had bugfixes that were never released before a minor/major
release was cut, you'll need to merge the changelog entries for that release into the `develop`
branch's changelog. As an example, consider the following:

```markdown
## 2.6.0 - TBD

### Added

- Useful features that everyone will want.

### Changed

- Nothing.

### Deprecated

- Useless features that are no longer needed.

### Removed

- Nothing.

### Fixed

- Stuff that couldn't be fixed as they require additions.

## 2.5.3 - TBD

### Added

- Nothing.

### Changed

- Nothing.

### Deprecated

- Nothing.

### Removed

- Nothing.

### Fixed

- A bunch of stuff that was broken
```

The above would be merged to a single changelog entry for 2.6.0 which would look like this:

```markdown
## 2.6.0 - TBD

### Added

- Useful features that everyone will want.

### Changed

- Nothing.

### Deprecated

- Useless features that are no longer needed.

### Removed

- Nothing.

### Fixed

- Stuff that couldn't be fixed as they require additions.
- A bunch of stuff that was broken
```
