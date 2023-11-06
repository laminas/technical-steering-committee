# Next Technical Steering Committee Meeting Agenda

- Date: 2023-11-06
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Abandon `laminas-crypt`

In [laminas-crypt#32](https://github.com/laminas/laminas-crypt/pull/32) @Xerkus writes:

> This component is security only. Since it has no maintainer and it is a security oriented component may be it should be abandoned instead.
> 
> ...
> 
> Providing cryptographic solution implies we have the necessary expertise to ensure it is not done in a flawed manner and it is secure against emergent flaws and vulnerabilities discovered since the original implementation.

Components that [currently depend](https://github.com/laminas/laminas-crypt/network/dependents?owner=laminas&dependent_type=REPOSITORY&owner=laminas) on `laminas-crypt`

- laminas-twitter - requires laminas-oauth
- laminas.dev - Getting rid of twitter stuff here will remove the dependency
- laminas-oauth - in security only mode
- laminas-mail ([Release 2.24.0](https://github.com/laminas/laminas-mail/releases/tag/2.24.0) removes dependency)
- laminas-filter _(Version 3 [unreleased], will no longer depend on it)_
- laminas-authentication [PR #55](https://github.com/laminas/laminas-authentication/pull/55) negates dependency requirement but needs review on whether the approach is acceptable.

### Proposal to abandon and archive [laminas-twitter](https://github.com/laminas/laminas-twitter)?

George Steel asks, is it feasible to continue to support this library now that read access is a paid only feature?

`laminas-twitter` also depends on `laminas-crypt` which may or may not be considered for abandonment too.

## Abandon `laminas-oauth`

George Steel proposes we also abandon laminas-oauth, as it is only used by laminas-twitter internally.
