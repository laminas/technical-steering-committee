# Technical Steering Committee Voting Process

While the Project aims to operate as a consensus-based community, many decisions
will require a vote in order to move forward: approval of new repositories
or subprojects, approval of archival/abandonment of repositories or subprojects,
approval of new maintainers, selection of Project Lead, etc.

Voting will happen either within a meeting, or via electronic vote.

For purposes of this document, when 50% results in a fraction, `ceil(50%)` is
implied.

## TSC Meeting Votes

Meetings will happen on the first Monday of each month. An agenda will be
provided in the repository, with the ability for anybody to request an item be
added, modified, or removed via pull request.

Per the charter, quorum for a meeting requires at least 50% of all TSC members
present. If quorum is not met, the meeting may continue, but no votes or
decisions may be made.

A vote may be called during a meeting. Such votes pass only if a simple majority
of those present in the meeting approve. If a vote passes, but does not
receive 50% of all TSC members (not just those present) approving, we will hold
an asynchronous electronic vote to validate the decision.

## Asynchronous Electronic Votes

A vote may be initiated outside meetings, using technologies such as Google
Forms or [ADoodle](https://adoodle.org); anonymous votes are encouraged, but
all voting results must be published publicly on completion (per the charter).
In such cases, per the charter, a decision is only binding if at least 50% of
all TSC members approve.

The voting period for asynchronous votes is 2 weeks, or until all TSC members
have voted, whichever comes first.

## Decisions requiring a vote

The following list is non-exhaustive.

- Approval of new Maintainers (only requires a simple majority approval).
- Approval of a new TSC member.
- Selection of Project Lead.
- Acceptance of a new repository to the Project or a subproject.
- Acceptance of a new subproject.
- Abandonment of a repository.
- Abandonment of a subproject.
- Approval of a cross-repository or cross-project initiative.
- Expulsion of any Maintainer, TSC member, or the Project Lead.
- Releasing a new major version of a subproject _may_ require a vote. This is detailed in ["Major Releases"](#major-releases)

## Major Releases

In order to publish a backwards incompatible major release, it is _required_ that the maintainer who intends to make the release will send a notification to the TSC members "Private Channel" _(currently this is hosted in Slack)_.

This notification should include the repository name and the intended release date, which must be at a minimum of 2 weeks after the date of notification.

The purpose of this process is to ensure that TSC members have the time to voice any concerns, address any outstanding quality issues or introduction of additional BC breaks _(for example)_.

This 'cooling off' period also allows TSC members to request the release be subject to a vote in an upcoming TSC meeting. This may be necessary when there are significant architectural changes that warrant greater attention.

If a member wishes to escalate the release decision to a vote, it is expected that this member will add the item to the [meeting agenda](../meetings/agenda.md) and communicate this with the member(s) responsible for the release.

In normal circumstances, where there are no objections within the 2-week window, the member responsible for the release may feel free to publish the major revision on or after the expected date.
