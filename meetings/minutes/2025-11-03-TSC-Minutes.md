# Minutes from the 2025-10-06 Laminas Technical Steering Committee Meeting

- When: 2025-11-03 at 19:00 UTC, until 19:47 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - George Steel
    - Julian Somesan
    - Luís Corbucci
    - Matthew Weier O'Phinney
    - Rob Allen

Quorum WAS NOT met (7 out of 16 members were present).

## Agenda


### Package archival and PHP constraint

When archiving packages, should we switch the PHP dependency to use the `^` constraint instead of `~` to allow it to be used by consumers until the PHP version goes EOL?

#### Discussion

General consensus is that this would simplify consumption by end-users, eventually forcing them to either stop using these packages if they want to adopt a new PHP major version, or to fork the code themselves to provide support for that new major.

### Immutable releases

Should we adopt GitHub's immutable releases feature?

#### Discussion

Aleksei is a bit skeptical of the feature, as GitHub doesn't fully prevent release and tag removal with this feature, just re-issuing them. Matthew pointed out that the feature is only for releases made _after_ the feature is enabled, but Aleksei pointed out that the backing tag can still be removed, and that the main security feature is the ability to provide attestations for release assets — which would require that we build them ourselves instead of letting GitHub do it.

Julian pointed out that the workflow is to create a draft release, attach all assets, and then publish the draft, which might require changes to automatic-releases. Luís noted that he's actually used automatic-releases on some repos he owns where he's enabled the feature, and it worked fine.

This then means that the primary benefit is that the tag cannot be swapped with new content — which is likely a good goal regardless.

Matthew asked if GH generates attestations, or if we would need to create and sign our own packages. Aleksei notes that the `gh` CLI command has a `release verify` subcommand that can be used to validate a release, so the attestation must be attached to release metadata somehow. Again, this would be a net benefit.

The main issue is that if a rogue user or attacker were to mass delete tags and/or releases, we would not be able to recreate them without intervention from GitHub. However, the mitigation of risk for end users makes it a no-brainer.

Aleksei recommended we wait a short while for others to adopt the feature and iron out the edge cases.
