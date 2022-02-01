# Minutes from the 2021-12-06 Laminas Technical Steering Committee Meeting

- When: 2021-12-06 at 19:00 UTC, until 20:29 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Bruchner
  - Matthew Weier O'Phinney
  - Maximilian Bösing
  - Michał Bundyra
  - Rob Allen

Quorum was NOT met (7 out of 15 members were present).

## Agenda

### Should we adopt reusable workflows

- Reference: https://github.blog/2021-11-29-github-actions-reusable-workflows-is-generally-available/
- We could simplify our CI setup even further, hiding the "matrix" that we generate
- We could make the automatic-releases workflow a bit smaller to integrate
- We could introduce some automations for tweeting/publishing releases to outside the organization
- We could introduce "branch cleanup" actions that delete branches for which our maintenance policy no longer covers support
- We could automate dependency upgrades

Rob Allen started discussion with the question of "how much effort is required vs the amount of changes that are made?", with Max following up with "I wonder how that would look like?", positing that the main benefits just don't work with our current actions and workflow setups, particularly as it would mean that we would have to touch all the various repositories _again_.

Matthew answered that while we'd have the up-front effort, we'd have _less_ effort later if we wanted to roll out changes to our workflows (with the examples of adding a "notify twitter" step to a release, or a "notify slack" step to a failed build).
Rob pointed out this may be a YAGNI thing, and Matthew agreed, as the point of the new workflows we have was largely to make it so we won't need to update repositories when workflows change; they end up being handled in the actions we reference in the workflows themselves.
At this point, Rob suggested that we've done a lot of infrastructure work this past year to streamline our processes, and doing more has diminishing returns, to which there was broad agreement.

Max was curious how reusable workflows work, to which Aleksei pointed out some concrete examples.
One thing that piqued people's interest was the fact that re-use refers to the repository and a reference, which helps with predictability and stability.
Additionally, you can provide inputs (including secrets) and use outputs from them.

Matthew suggested that we:

- develop the reusable workflows and push them to the `.github` repo
- new packages would consume the reusable workflows
- if/when we think about it, we can update existing packages to use them

This got solid agreement.

### Should we try and automate dependency upgrades via @dependabot?

- Automating composer dependencies upgrades with @dependabot, and the noise it would cause in email notifications.
  It is necessary, but a solution that doesn't overwhelm maintainer inboxes is somehow needed.
- Automating patches to upgrade PHP versions?
  That would save us quite a lot of work in 2022.

Abdul suggested this would be really nice when coupled with an "auto merge if CI is green" policy.

Aleksei noted that Dependabot tends to be extremely spammy in nature, making it easy to start categorizing its notifications as "noise" and ignoring them.
Max said that it _can_ be configured to be less noisy, and noted that you can even specify different intervals so that it doesn't check as frequently (e.g., weekly or monthly instead of daily).
Aleksei pointed out it creates a PR per updated dependency, then rebases as you merge, creating lockfile conflicts; he had 400+ PRs created in a 4 months span on a relatively small Mezzio application when using a 2 week schedule.
His opinion is that Renovate bot is a better solution, as it supports bumping all deps at once.

Max reframed the conversation to talk about how these solutions could benefit the project, particularly around the release of new PHP mnor or major versions.
A solution like this could be run weekly, adding PHP nightly builds to the matrix, and thus notify us early of BC issues.
Max noted that one consideration is that PHPUnit changed the default of the `convertDeprecationsToExceptions` flag to disabled, which means we would need to somehow enable that on these runs if it is not already enabled via `phpunit.xml.dist`.
Aleksei suggested it would look something like this:

- Regular scheduled nightly workflow in every repo
- Calls a central re-usable workflow
- Re-usable workflow is a no-op until nightlies are available
- Reusable workflow updated to run nightly with an override flag for the matrix builder
- All repos start doing scheduled builds at this time
- After the stable PHP release happens, the workflow is back to a no-op state

Which sounds like a lot of work.

Matthew noted that our own CI will trigger when a PR is opened that expands the PHP version constraint.
Gary Lockett (community member) noted that Renovate can do exactly this: run on a scheduled basis, detect a new PHP nightly/alpha/beta/rc is available, and open a PR that widens the PHP version constraint as a result.
It would then be a matter of us having support for that new PHP version in our CI container.

Matthew suggested somebody create a plan that:

- Outlines pros and cons
- Develops a methodology
- Details what roll-out would look like
