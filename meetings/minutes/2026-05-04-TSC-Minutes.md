# Minutes from the 2026-05-04 Laminas Technical Steering Committee Meeting

- When: 2026-05-04 at 19:00 UTC, until 20:27 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - Frank Brückner
    - George Steel
    - Julian Somesan
    - Rob Allen

Quorum WAS NOT met (6 out of 16 members were present).

## Agenda

### Clarification of Vote Requirement for Major Releases (By _@gsteel_)

The TSC members discussed what types of releases require votes from the TSC team.

#### Discussion

George and Rob agree that not all releases are the same, so they don't all require voting.

Aleksei argued that normally, the update author, maintainer and an additional TSC member should be enough to confirm a release.
He added that some updates don't require TSC involvement: updating dependencies, language features, removing deprecations.
He believes that major rewrites (e.g., for laminas-view, service manager) should be reviewed by a second TSC member not involved in the update.

George prefers to review his changes in the TSC meetings.
Rob believes that the TSC team be notified 2 weeks before major releases.
If there is no additional input, the release can go forward.

#### Decisions

The [voting process document](https://github.com/laminas/technical-steering-committee/blob/main/processes/VOTING.md#major-releases) has been updated to cover scenarios for major releases.

### Clean up the Member List

The TSC members list contains people who aren't active anymore.
The members should decide if they can be removed, which would also free up space for other nominations.

#### Discussion

Julian mentioned that this issue was considered before and that new nominations can be made, even without editing the current TSC member list.
Rob suggested they remove entries from the list from people who haven't attended TSC meetings in more than 6 months.
Aleksei added that inactive members should also have their merge rights revoked.
Julian and Aleksei agreed to build a list for TSC members that should be removed from the [current list](https://github.com/laminas/technical-steering-committee/blob/main/MEMBERS.md).

George mentioned that each member to be removed must be voted separately.
Aleksei added that all members on the list should be contacted to attend the TSC meeting or be considered for removal from the list in 2 months.
Rob agreed that checking the TSC minutes is the easiest way to see member activity.

#### Decisions

Build a list containing each member on the TSC list, with their last TSC meeting attendance.
Then review and decide upon each entry via a poll in future TSC meetings.
An async poll was opened and passed with the question: **Should we propose the removal from the TSC Members list of anyone who did not attend a meeting in the past 12 months?**

### Speed up the release of ServiceManager v4 support in downstream packages (By _@arhimede_)

Julian argues that certain highly expected releases to the Laminas packages have seen long delays.
He suggests a 2-lane approach:

- A fast lane: prioritize Service Manager v4 (SM4) implementation for a new release that can be made sooner.
- A slow lane: release other core, BC-breaking updates when ready.

#### Discussion

Rob and George agreed that working on both SM4 and major BC work at the same time was too optimistic.
George added that the additional work was required because of legacy-mutable states in the codebase.

Julian mentioned that several packages are behind on the SM4 support:

- [laminas-session](https://github.com/laminas/laminas-session)
- [laminas-inputfilter](https://github.com/laminas/laminas-inputfilter)
- [laminas-form](https://github.com/laminas/laminas-form)
- [laminas-hydrator](https://github.com/laminas/laminas-hydrator)
- [laminas-i18n](https://github.com/laminas/laminas-i18n)

George mentioned that he would rather release his work on `laminas-inputfilter` together, even if it impacts `laminas-form`.
He added that MVC-related libraries would not get SM4 support.
Julian offered to have members from his team help with the SM4 updates.

#### Decisions

The members agreed that SM4 support should be prioritized for future releases, where needed.
