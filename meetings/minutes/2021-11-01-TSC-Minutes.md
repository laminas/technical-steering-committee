# Minutes from the 2021-11-01 Laminas Technical Steering Committee Meeting

- When: 2021-11-01 at 19:00 UTC, until 21:28 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl (left shortly after 20:00)
  - Luís Cobucci (left shortly after 20:00)
  - Matthew Weier O'Phinney
  - Rob Allen

Quorum was NOT met (6 out of 15 members were present).

## Agenda

### Require `GITHUB_TOKEN` permission to be explicitly specified in GHA workflow files

Permissions for `GITHUB_TOKEN` are [too broad and provide write access to a number of scopes](https://docs.github.com/en/actions/reference/authentication-in-a-workflow#permissions-for-the-github_token) when action is run in a privileged context of a maintainer.
Such privileged context is invoked, for example, on branch push event after the PR was merged.
This poses a security risk in case of supply chain attack or vulnerability in invoked dependencies (eg [CVE-2021-29472 for Composer](https://nvd.nist.gov/vuln/detail/CVE-2021-29472)).

[Aleksei](https://github.com/Xerkus) proposes to make the [permissions](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#permissions) field mandatory in all workflow files in all Laminas repositories with only required privileges specified for the specific workflow.

> ```yaml
> permissions:
>   actions: read|write|none
>   checks: read|write|none
>   contents: read|write|none
>   deployments: read|write|none
>   issues: read|write|none
>   packages: read|write|none
>   pull-requests: read|write|none
>   repository-projects: read|write|none
>   security-events: read|write|none
>   statuses: read|write|none
> ```

[Matthew](https://github.com/weierophinney) asked for some clarifications on how this works exactly, and the following items were noted:

- We set the default permissions at the repository level.
  By default, they are read-write, but we would make them read-only.
  Doing so implicitly does this to all workflows and jobs:

  ```yaml
  permissions:
    actions: none
    checks: none
    contents: read
    deployments: none
    id_token: none
    issues: none
    discussions: none
    packages: none
    pull-requests: none
    repository-projects: none
    security-events: none
    statuses: none
  ```

- A workflow and/or a job would override permissions via a `permissions` block (as noted above) if write permissions are necessary.

As an example, the docs-build workflow would add:

```yaml
permissions:
  contents: write
```

as it needs to write back to the gh-pages branch.

Workflows such as the automatic-releases workflow would be largely unaffected, as they pull in an organization token with scoped permissions already via organization secrets.

Matthew asked Aleksei to:

- Do some experiments to determine what permissions are needed per workflow (CI, automatic releases, docs-build)
- Create a proposal that demonstrates the changes required for existing workflows

Once the proposal is in place, we can vote on it, as general consensus is this is a fairly straight-forward and understandable security tightening measure for us.

### PHPUnit Change Regarding Deprecation Reporting

With `phpunit/phpunit` [v8.5.12](https://github.com/sebastianbergmann/phpunit/blob/c814a05837f2edb0d1471d6e3f4ab3501ca3899a/ChangeLog-8.5.md#8521---2021-09-25) as well as [v9.5.10](https://github.com/sebastianbergmann/phpunit/blob/c814a05837f2edb0d1471d6e3f4ab3501ca3899a/ChangeLog-9.5.md#9510---2021-09-25), the way on how PHPUnit treats deprecations by default changed.

In earlier versions, deprecations where triggered as exceptions.
With these versions, this was disabled by changing the configuration flag `convertDeprecationsToExceptions` was changed from `true` to `false`.

[Matthew](https://github.com/weierophinney) somewhere stated that its good that Laminas CI tests do fail when a deprecation is hit.
The rationale for this is that we would be able to handle deprecations early on.
If we handle deprecations early on, the overall tech-debt when adding support for a new PHP major version (where deprecations usually lead to errors) will be lower which then prevents dirty hacks to do a balancing act between multiple major versions.

Since most deprecations are not required to be changed when initially supporting a new PHP version, [Marco](https://github.com/Ocramius) and [Axel](https://github.com/tux-rampage) are fine with keeping the `convertDeprecationsToExceptions` flag disabled while [Max](https://github.com/boesing) tends to agree with Matthew in fixing deprecations as early as possible.

Our choices to discuss during the meeting:

1. Keep the "old way" which treats deprecations as build errors by re-enabling the old PHPUnit behavior (by [merging and releasing the PoC](https://github.com/laminas/laminas-continuous-integration-action/pull/54) provided by Max).
2. Fully ignore the fact that there are PHP deprecations which lead to errors until when they are leading to errors.
3. Find another solution which fits both points.

A possible different solution could be to have an action which checks for PHP deprecations only, may fail and if it fails, an issue is created in the repository so we are at least aware of that there are deprecations which should be addressed.

There are actually ways to mark actions as required or optional via branch protection rules.
Maybe this is something we can do when adding support for new PHP versions.

[Andreas](https://github.com/heiglandreas) suggested we create a mechanism to convert deprecations into issue reports, so that we can tackle them separately from other work.
[Luís](https://github.com/lcobucci) favors option 1 and would not recommend option 2, for the same reasons Matthew argued; he also notes that in some cases, what we are treating are deprecations triggered by external dependencies.
Aleksei noted that we even sometimes trigger deprecation notices ourselves, and have traditionally had tests that validate this fact. Nobody felt that option 2 was viable.

Luís suggests that while we could make option 1 the rule, we could and likely should still setup CI on a schedule, and have it report deprecations as issues.
This would help identify deprecation issues early and provide a way of tracking when we fix the issues.
It also more easily helps us address those outside of other patches.
If we do this, we could actually have separate configuration for normal pull request runs versus scheduled runs, which would simplify contributions, but also ensure we address the deprecations.
Since PHP releases happen roughly monthly, a monthly job would likely be sufficient.

At this point, Matthew summed everything up:

- Nobody is okay with just ignoring deprecations entirely and waiting for actual breakage.
- There's some consensus that a continue-on-error job that toggles `convertDeprecationsToExceptions` on and creates issues on detecting deprecation errors could be good, but we'd need to ensure this is done in a robust way that doesn't create too many false positives.
- Scheduled jobs would be another way to notify maintainers (either via created issues, or via how GH notifies maintainers of failed builds) of deprecation errors and ensure that they do not block other contributions.

Luís volunteered to work up a prototype and a proposal.

### Where would we like to invest?

We have accumulated close to $20k (USD) in donation so far, and should start thinking of where we want to invest them.
Some ideas include:

- Providing stipends/honorariums to maintainers.
- Sponsoring user groups and/or conferences.
- Funding some short-term, targetted initiatives (e.g., finishing up and releasing MVC 4, creating documentation tutorials, OpenAPI parsers/generators, etc.)
- Creating swag to send to contributors.

This part quickly derailed, with folks suggesting sending invoices to the foundation, or using it at the gambling table. :rofl:

Andreas suggested paying somebody to bring the documentation up to speed, which was met with some enthusiasm.
[Rob](https://github.com/Akrabat) suggested augmenting this with video tutorials if possible as well.

Rob went on to suggest CLI tooling: things like CRUD scaffolding, code generation from OpenAPI specifications, etc.
His point is that better documentation, adding videos, and providing more tooling will help us attract and keep users.

At this point, people were neeing to leave.
Matthew suggested that we potentially do a quick community survey to see what people would find most valuable, so we can start putting money towards those initiatives.
