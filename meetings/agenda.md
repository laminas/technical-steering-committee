# Next Technical Steering Committee Meeting Agenda

- Date: 2021-09-06 or 2021-09-13 (TBD)
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Require `GITHUB_TOKEN` permission to be explicitly specified in GHA workflow files

Permissions for `GITHUB_TOKEN` are [too broad and provide write access to a number of scopes](https://docs.github.com/en/actions/reference/authentication-in-a-workflow#permissions-for-the-github_token) when action is run in a privileged context of a maintainer. Such privileged context is invoked, for example, on branch push event after the PR was merged. This poses a security risk in case of supply chain attack or vulnerability in invoked dependencies (eg [CVE-2021-29472 for Composer](https://nvd.nist.gov/vuln/detail/CVE-2021-29472))

I propose to make [permissions](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#permissions) field mandatory in all workflow files in all Laminas repositories with only required privileges specified for the specific workflow.

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

### PHPUnit Change Regarding Deprecation Reporting

With `phpunit/phpunit` [v8.5.12](https://github.com/sebastianbergmann/phpunit/blob/c814a05837f2edb0d1471d6e3f4ab3501ca3899a/ChangeLog-8.5.md#8521---2021-09-25) as well as [v9.5.10](https://github.com/sebastianbergmann/phpunit/blob/c814a05837f2edb0d1471d6e3f4ab3501ca3899a/ChangeLog-9.5.md#9510---2021-09-25), the way on how PHPUnit treats deprecations by default changed.

In earlier versions, deprecations where triggered as exceptions. With these versions, this was disabled by changing the configuration flag `convertDeprecationsToExceptions` was changed from `true` to `false`.

Matthew ([@weierophinney](https://github.com/weierophinney)) somewhen stated, that its good that laminas CI tests do fail when a deprecation is hit. The rationale for this is, that we would be able to handle deprecations early on. If we handle deprecations early on, the overall tech-debt when adding support for a new PHP major version (where deprecations are usually lead to errors) will be lower which then prevents dirty hacks to do a balancing act between multiple major versions.

Since most deprecations are not required to be changed when initially supporting a new PHP version, Marco ([@Ocramius](https://github.com/Ocramius)) and Axel ([@tux-rampage](https://github.com/tux-rampage)) are fine with keeping the `convertDeprecationsToExceptions` flag disabled while Max ([@boesing](https://github.com/boesing)) tends to agree with Matthew in fixing deprecations as early as possible.

What we should discuss during the TSC meeting is if we want to:

1. keep the "old way" which treats deprecations as build errors by re-enabling the old PHPUnit behavior (by [merging and releasing the PoC](https://github.com/laminas/laminas-continuous-integration-action/pull/54) provided by Max)
2. fully ignore the fact that there are PHP deprecations which lead to errors until when they are leading to errors
3. find another solution which fits both points

A possible different solution could be to have an action which checks for PHP deprecations only, may fail and if it fails, an issue is created in the repository so we are at least aware of that there are deprecations which should be addressed.

There are actually ways to mark actions as required or optional via branch protection rules. Maybe this is something we can do when adding support for new PHP versions.
