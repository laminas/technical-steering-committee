# Minutes from the 2023-11-06 Laminas Technical Steering Committee Meeting

- When: 2023-11-06 at 19:00 UTC, until 19:38 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - George Steel
  - Matthew Weier O'Phinney
  - Maximilian Bösing
  - Michał Bundyra
  - Rob Allen

Quroum WAS met (9 out of 15 members were present).

## Agenda

### Abandon `laminas-crypt`

In [laminas-crypt#32](https://github.com/laminas/laminas-crypt/pull/32) [@Xerkus](https://github.com/Xerkus) writes:

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

#### Discussion

There was basically no dissent; everyone agreed we should abandon it.
The main concerns were around impact on other components, particularly on laminas-mail, but George and Matthew demonstrated that the CRAM-MD5 functionality in that component can be addressed solely with the built-in `hash_hmac()` function.
Likewise, other places where the functionality is needed, it's likely best to inline it in those components, as it future-proofs them and simplifies integration testing.

Consensus was summed up by Matthew and Aleksei, who both noted that without cryptographic experts on the steering committee or in our maintainers roster, it's a disservice to our users, who could be exposed to vulnerabilities, particularly if the default algorithms become outdated or easily compromised.

Discussion turned then to laminas-oauth, as that's the primary component still requiring laminas-crypt.

Rob pointed out that if somebody is using OAuth1 still, they've likely moved to a maintained component.
Matthew pointed out that the only real reason laminas-oauth has continued to be maintained is due to the fact laminas-twitter uses it... which is already a topic for abandonment (see next topic in these meeting minutes).

#### Decisions

We held two separate polls, one to abandon laminas-crypt, another to abandon laminas-oauth.
Both polls received unanimous support; we will archive both and mark them abandoned on Packagist.

### Proposal to abandon and archive [laminas-twitter](https://github.com/laminas/laminas-twitter)?

George Steel asks, is it feasible to continue to support this library now that read access is a paid only feature?

`laminas-twitter` also depends on `laminas-crypt` which may or may not be considered for abandonment too.

#### Discussion

There wasn't any.

The topic had been brought up during the laminas-crypt topic, and consensus was to abandon it as well.
There were already concerns as we cannot test against the API to verify changes (costs too much), and the API documentation is no longer being kept up-to-date with changes.

#### Decision

We held a poll, and 8 members voted to abandon laminas-twitter, and 1 voter indicated they were undecided.
8 voters met our 50% + 1 requirement, so the measure passed.

#### Actions

Matthew volunteered to do the following:

- Publish the minutes (here)
- Update the `README.md` files for each component to (a) message that we're abandoning the component, and why, and (b) link to these minutes.
  In the case of laminas-oauth, we will also recommend [League OAuth 1.0 Client](https://github.com/thephpleague/oauth1-client).
- Update the `composer.json` of each package to add the `abandoned` field, setting the value to a recommended package if one is known.
- Archive each component on GitHub when the above is done.
