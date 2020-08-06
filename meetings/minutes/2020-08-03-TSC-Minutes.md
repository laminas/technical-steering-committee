# Minutes from the 2020-08-03 Laminas Technical Steering Committee Meeting

- When: 2020-08-03 at 19:00 UTC, until 20:39 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Geert Eltink
  - James Titcumb
  - Luís Cobucci
  - Marco Pivetta
  - Max Bösing
  - Michał Bundyra
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Rob Allen

Quorum was met (13 out of 15 members were present).

## Agenda

- New branch model on security-only repositories?
  ([jump to discussion](#apply-new-branching-model-to-security-only-components))

  As we are about to mark packages to receive security-only fixes, @boesing
  would like to discuss if we want to apply the new branch model (related to the
  new release-process) to those repositories as well or if we exclude these?

- Vote on components to mark security only.
  ([jump to discussion](#vote-on-components-to-mark-as-security-only))

  Since we did not get 100% of the TSC to vote on the components to mark as
  security-only, we need to vote on them during the meeting. As a reminder, they
  are:
  
  - laminas/laminas-barcode
  - laminas/laminas-config
  - laminas/laminas-config-aggregator-modulemanager
  - laminas/laminas-console
  - laminas/laminas-crypt
  - laminas/laminas-db
  - laminas/laminas-dom
  - laminas/laminas-file
  - laminas/laminas-http
  - laminas/laminas-json
  - laminas/laminas-loader
  - laminas/laminas-log
  - laminas/laminas-mail
  - laminas/laminas-math
  - laminas/laminas-memory
  - laminas/laminas-mime
  - laminas/laminas-mvc-console
  - laminas/laminas-oauth
  - laminas/laminas-progressbar
  - laminas/laminas-serializer
  - laminas/laminas-servicemanager-di
  - laminas/laminas-soap
  - laminas/laminas-tag
  - laminas/laminas-text
  - laminas/laminas-uri
  - laminas/laminas-xml
  - laminas/laminas-xml2json

- @weierophinney proposes a by-law change to require only 2/3 of members vote
  for asynchronous votes. This ensures that if any member is unable to be
  present, we do not need to wait until the next TSC meeting to hold a vote.
  ([jump to discussion](#discuss-async-voting-quorum-requirements))

- Vote on adopting a static analysis tool: Psalm vs phpstan
  ([jump to discussion](#vote-on-static-analysis-tooling))

## Apply new branching model to security-only components

Max wanted to know if we should apply the new branching model and automatic
releases workflow [as agreed upon last month](2020-07-06-TSC-Minutes.md) to
components we decide to mark as security-only.

There was very little discussion. The initial, and standing, consensus was that
we should only apply it to those repositories **if** we need to make a release
on them. Considering migrating to the automatic-releases workflow is trivial,
doing so as part of a patching process will not add undue burden.

**We held a vote, which passed unanimously, to only adopt the automatic-releases
workflow and branching strategy on security-only components if a release is
warranted.**

## Vote on components to mark as security-only

Matthew (@weierophinney) noted that we did not have all members voting during the
out-of-band/async vote held last month on which components to mark as
security-only. As such, it was non-binding.

We had some initial discussion about whether the voting by-law needs to be
revisited, to which Matthew pointed to the next agenda item.

When we resumed discussion, there were a few points brought up:

- Some components listed are still actively used, but feature-complete, and
  maintainers were a bit reluctant to mark them "security-only". We agreed that
  such components could use the verbiage "This package is considered feature
  complete. It is now in security-only maintenance mode."

- When looking at the [results of the security-only vote](https://adoodle.org/index.php?action=showresults&survey=35da670eb1f5f549f88989c65ea8a266),
  none of the votes were close; in all cases, we had > 60% of voters voting to
  mark each component as security-only, and most were in the > 70% and > 80%
  range.

In the end, **we voted to accept the results of the async vote held last
month.** As such, all of the components listed will go into security-only mode,
and receive no new bugfixes unless we have maintainers step up with concrete
plans for maintaining and evolving the component.

## Discuss async voting quorum requirements

Matthew (@weierophinney) read [section 3(c) of the charter](../../CHARTER.md#3-tsc-voting)
to mean that 100% of TSC members must vote if an electronic vote (vote held
outside a TSC meeting) is held, which is why he wanted a new vote on the
security-only components. He proposed changing the by-law to only require 2/3 of
TSC members to vote during an electronic vote.

We started noting that votes held during a TSC meeting require a quorum of 50%
of members, and only require a simple majority to pass. This means as few as 1/3
of members voting during a meeting could result in a measure passing. During
discussions we clarified for all members that _quorum_ is a minimum number of
members necessary to hold a meeting or vote, and _simple majority_ means any
value > 50%. Additionally, we agreed that any fractions imply `ceil()`, to
ensure the minimum threshold is met.

When asked why he proposed a 2/3 quorum for electronic votes, Matthew indicated
this is the threshold used by PHP-FIG, to resolve issues that occurred when too
few people were voting, resulting in measures that didn't have broad consensus
passing.

Rob noted that we likely need to consider un-inviting TSC members in the future
who are not active, as it changes the quorum threshold. James asked for a
definition of "active", to which Rob responded "vote in at least one of the last
5 sessions of voting". Matthew (MWOP) noted that this is likely a good
discussion to have, but off-topic for now.

At this point, Aleksei pointed out that the charter reads:

> Decisions made by electronic vote without a meeting require a majority vote of
> all voting members of the TSC.

He pointed out it doesn't say that all members must vote, only that the vote
requires at last 50% of TSC members choosing a specific option to be binding. As
we discussed this, we boiled it down to this example: if we have 15 members, and
8 members participate in a vote, and all vote the same, then that vote is
accepted.

Andreas asked at this point about what it means to **abstain** from voting. We
agreed that:

- Abstain votes count towards quorum.
- Abstaining indicates the voter either does not have enough information to make
  a decision, or is willing to go with the majority decision.
- We need to ensure we have an "Abstain" option whenever we initiate a vote.

When we continued discussions, two points were brought up we wanted to clarify:

- The charter mentions "voting members of the TSC", which implies there are
  multiple "classes" of TSC membership. There are not.
- Currently, the charter allows for a simple majority of a simple majority
  (i.e., 25%) to make a vote binding if the vote is held in-meeting. This means
  it has a lower threshold than async votes.

**In the end, we voted to make the following changes:**

- **We will disambiguate the by-laws for online votes to indicate that 50% of TSC
  members must vote for an option for it to be binding.**
- **We will disambiguate that "50%" means ceil() of 50% of TSC members.**
- **We will add a note somewhere in the by-laws/processes that if a vote passes
  during meeting, but does not get 50% of TSC members approving, we will hold an
  async vote to validate.**

## Vote on static analysis tooling

The last item on the agenda was a vote to select which static analysis tool we
will standardize on, [Psalm](https://psalm.dev) or [PHPStan](https://phpstan.org).

A question was asked: why not both? The main rationale is to simplify what
contributors and maintainers need to know; when there are multiple tools, more
knowledge is needed, which can act as a barrier to contribution.

Marco is a proponent of (and contributor to) Psalm. His rationale for selecting
it were:

- PHPStan's reliance on "magic plugins" makes understanding flagged errors more
  difficult, and can lead to conflicts between them. On top of that, plugin
  manipulation of types can allow end-users to omit type documentation, making
  understanding what is expected harder.

- Psalm forces documenting types in detail, at the code level, giving
  maintainers a better understanding of what types are being used.

- Psalm's type inference is far better than competitors.

- Psalm's default settings already enforce the majority of what we want.

- Development on Psalm is outpacing that of PHPStan.

Consensus amongst those present is that, overall, Psalm tends to have fewer
false positive error detections, and also provides more actionable feedback to
the consumer on how to resolve issues.

**We voted to adopt Psalm as our standard static analysis tool.**

## Summary

This was a somewhat shorter meeting (running just over 1.5 hours, versus the 2.5
hours last month). We anticipate seeing more voting occurring outside meetings
due to our clarifications to the by-laws. In the meantime, we will be marking a
number of components as being in security-only status, and starting to introduce
Psalm into our QA workflow.
