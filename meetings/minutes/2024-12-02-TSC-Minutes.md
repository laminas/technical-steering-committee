# Minutes from the 2024-12-02 Laminas Technical Steering Committee Meeting

- When: 2024-12-02 at 19:00 UTC, until 20:05 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Frank Brückner
    - George Steel
    - James Titcumb
    - Julian Somesan
    - Luís Cobucci
    - Matthew Setter
    - Michał Bundyra

Quorum WAS met (8 out of 16 members were present).

## Agenda

### New major version of laminas-di

[@tux-rampage](https://github.com/tux-rampage) proposed that laminas-di should receive a new major version to improve its future maintainability and to support new PHP features.

#### Discussion

Julian recommended to keep support for at least PHP 8.2 in all packages, including laminas-di.
PHP 8.2 is supported until the end of 2024, but the security support for the same version is until 2026.
Luís and George reviewed PHP 8.2 and 8.3 and concluded that dropping support for those versions is not warranted.

#### Decisions

The members agreed that voting is not required.
Instead they can comment on the RFC issue and its future PR from @tuxrampage.

### Release Mezzio Router v4

George made a thorough check on the [roadmap for mezzio-router v4](https://github.com/mezzio/mezzio-router/issues?q=is%3Aclosed+milestone%3A4.0.0) and concluded the component is ready to be released.

#### Discussion

Julian mentioned the inclusion of laminas/laminas-coding-standard v3 and George comfirmed it's already in mezzio-router v3.x as well.
Luís reminded the TSC members he is still working on FastRoute 2 which will simplify the mezzio adapter for it, so he is concerned about BCs.
George replied that future minor version for mezzio-router v4 can be released to handle BS changes in FastRoute.

#### Decisions

Julian created an async vote that passed the following day.

### Stale issue/PR cleanup proposal

[Alexis Karajos](https://github.com/alexmerlin) proposed a list of criteria to close PRs.

- Abandoned
- Targeting old branches
- Not linked with or created based on an existing issue

#### Discussion

George recommended the usage of [Close Stale Issues](https://github.com/marketplace/actions/close-stale-issues) to automate the closing of old issues and PRs.
Julian worried that PRs with important items might be lost, so a manual pass should be done first by Alexis.
George agreed that items should be first manually closed as needed, then a label should be assigned to items that shouldn't be closed.
The items that don't have the label would be closed automatically after a period of no activity.

#### Decisions

The members agreed that Alexis would check the existing items manually.
After he is done, the auto-closing strategy would be set up to close items after 6 months of no activity.
The strategy will be revised if needed.
