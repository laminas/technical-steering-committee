# Next Technical Steering Committee Meeting Agenda

- Date: 2021-09-06 or 2021-09-13 (TBD)
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Remove `laminas/laminas-zendframework-bridge` dependency from our packages

Over the past few weeks, we received multiple reports of people requesting us to drop `laminas/laminas-zendframework-bridge`
from our packages.

Our (TSC) response so far has been that we cannot do this until a new major version is released.
The reason for such a response is that people still rely on `Zend\` classes in their codebases, and therefore removal of `laminas/laminas-zendframework-bridge` could constitute a BC break for them, when a `laminas/` package substitutes a `zendframework/` one.

There may be a better solution to this though, which allows removal in a new **minor** release.

Here's an example for a hypotetical `laminas/laminas-xyz` package:

1. Remove the `{"replace": {"zendframework/zend-xyz": "self.version"}}` `replace`: block from `composer.json`:

   ```diff
   {
       ...
   -    "replace": {
   -        "zendframework/zend-xyz": "self.version"
   -    }
   }
   ```

2. Add a `conflict` with the old package in `composer.json`:

   ```diff
   {
       ...
   +    "conflict": {
   +        "zendframework/zend-xyz": "*"
   +    }
   }
   ```

3. Remove the `laminas/laminas-zendframework-bridge` dependency:

   ```diff
   {
       ...
       "require": {
           ...
   -        "laminas/laminas-zendframework-bridge": "^1.0"
       }
   }
   ```

4. Release under a new **minor** version (the `y` in `x.y.z`)

The proposed approach allows us to get a clean upgrade path for people that already use `laminas/*` packages, and already migrated away from the abandoned `zendframework/` packages.

People migrating from `zendframework/*` packages to `laminas/*` will still be able to use earlier **minor** releases of `laminas/*`, which we did release with the compatibility layer enabled.

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
