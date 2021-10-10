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
