# Minutes from the 2022-09-12 Laminas Technical Steering Committee Meeting

- When: 2022-00-12 at 19:00 UTC, until 20:36 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl (left after second agenda item)
  - Frank
  - Gary Lockett
  - George Steel
  - Luís Cobucci
  - Marco Pivetta (left after second agenda item)
  - Matthew Weier O'Phinney

Quorum WAS met (9 out of 15 members were present).

## Agenda

### Default git branching for new majors

When creating a new major, the relevant branch is created; it is also set as the default branch for the repository. However, there can be a significant gap between branch creation and the first release of that major version.

Contributors and renovate, will attempt to make bugfixes to this new major when they equally apply to the previous (current latest release) major.

I (ed: Gary Lockett) propose that the default branch should only be changed to the new major branch, once a release has been tagged for that new major.

#### Discussion

This had no debate; anybody who has had to maintain a repo that has an unreleased new major branch has run into the issue.
Matthew noted that we need automatic-releases to create the new minor branch when a new major branch already exists, as that's the root cause of the problem.
Aleksei noted that the logic should be "if the newly created branch version is higher than the current default branch, set the default to the new branch; otherwise, don't."

Matthew volunteered to create an issue on the automatic-releases repo to request this.

### Security only packages and dependency updates

Is this intention for security only packages to eventually be abandoned? If no, then should we look at ways to allow renovate to keep these up to date, if only to give us warning when the package may actually need maintenance. Currently any PR would be automatically closed, including the "Configure Renovate" PRs.

(Submitted by Gary Lockett.)

#### Discussion

This was a contentious topic.
There were arguments that security-only means no patches should be merged unless they are for security.
Others argued that supporting a new PHP version constitutes a security patch.
Some argued we should point users to replacements; however, not all security-only repos have replacements.
Matthew noted that he merged PHP 8.1 support patches last year, and Marco noted that he has occasionally merged new features and bugfixes when he's found the patches solid, and that it was easier to hit "merge" and to release than to provide the rationale for not merging to the submitter.

Luís pointed out that the decision to mark packages as security-only was to provide us (the TSC) focus.
He also quoted minutes from when we voted on the security-only status, pointing out that we should consider each of (a) what WE want to maintain, (b) what the COMMUNITY wants to use, and (c) what DIFFERENTIATES us from other projects.
We did not end up discussing these questions, but they did lead to another idea: equating "security-only" with "passive maintenance".
Doing so would imply that having Renovate run against these repositories and performing updates would allow us to release new versions of these packages when a new PHP release does not result in test failures.
When tests fail against a new PHP version, we can evaluate if it's something we want to manually fix, and, if not, open a vote to archive the package, indicating it has reached end of life.

We eventually took a vote on wether or not to take this approach, and it was unanimous amongst those present (9 of 14).

There were a few loose ends:

- Aleksei and Luís suggested we provide some verbiage to contributors/issue reporters around this change in the form of a pinned issue on each repository.
- Gary suggested we will need a slightly different version of the Renovate configuration to ensure we only bump new PHP versions.
- Aleksei and Matthew noted that the current auto-close workflow does not work.
  Abdul suggested an alternative.
  Aleksei also suggested we make a re-usable workflow for this that we can drop in to the various security-only repos, and which carves out exceptions for patches and issues submitted by Renovate.

The plan is:

- Matthew will provide Gary with verbiage for the pinned issue detailing what security-only/passive maintenance means.
- Aleksei will create a re-usable auto-closer workflow, and then provide Gary with details on how to configure it in repositories.
- Gary will roll out the Renovate configuration, add the auto-closer workflow, and create the pinned issue for each security-only repository.

### Introduce Package to De-Couple laminas-view from laminas-mvc

[@gsteel](https://github.com/gsteel/) suggests creating a new package to act as a bridge between `laminas-mvc` and `laminas-view` so that as part of a 3.0 release, `view` can become independent of `mvc`.

The need for this package is immediately apparent in the way that certain helpers shipped with `view` are highly `mvc` specific such as the Url View Helper.

The ultimate goal is that `laminas-mvc-view` would become a hard dependency for `laminas-mvc` and `laminas-view` would not depend on `mvc` at all.

Relevant [RFC can be found here](https://github.com/laminas/technical-steering-committee/issues/123)… and work in progress on the proposed package is at [gsteel/laminas-mvc-view](https://github.com/gsteel/laminas-mvc-view/pull/1).

#### Questions

- Is adding another package to the Laminas org acceptable? Or would it be preferable to add the code directly to `mvc`?
- There is a reasonable amount of configuration and factories etc inside `MVC` itself that could be hosted in the proposed package. Is it acceptable to extract code in MVC too, such as the various [View related factories](https://github.com/laminas/laminas-mvc/tree/4.0.x/src/Service)?

#### Discussion

Those still present at this point were largely in favor of the proposal.
Luís suggested we keep the existing namespace in the new package, but others pointed out that this makes the liklihood of naming collissions higher, and reduces opportunities for a gradual migration from the existing packages to the new package + existing packages.
Having a separate namespace allows the possibility of having the package available and able to coexist in existing applications before a new major version of either laminas-mvc or laminas-view; it's a necessary interim step.

Luís also asked if there's much liklihood that the new package will grow over time, or remain static; George and Matthew suggested that while it could grow, it's unlikely to grow significantly.

Since we no longer had quorum, the next step is an async vote within the TSC.
