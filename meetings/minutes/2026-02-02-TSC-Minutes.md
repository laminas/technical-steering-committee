# Minutes from the 2026-02-02 Laminas Technical Steering Committee Meeting

- When: 2026-02-02 at 19:00 UTC, until 20:08 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Aleksei Khudiakov
    - George Steel
    - James Titcumb
    - Julian Somesan
    - Matthew Weier O'Phinney
    - Michał Bundyra
    - Rob Allen

Quorum WAS NOT met (7 out of 16 members were present).

## Agenda

### Policy on "AI" Code Contributions

(Submitted by George Steel)

Whilst we have not received many contributions that have clearly been written by LLM tooling, I have personally encountered one _(So far)_.

Many among us, myself included have pretty strong opinions on LLMs and so-called "AI", and it makes sense that we develop a policy for dealing with contributions that use this type of tooling so that we can respond consistently.

We already have guidelines for automated submissions, but nothing that covers the copyright angle.

@jrfnl uses the following notice, which I thought was balanced and well written: https://github.com/PHPCSStandards/PHP_CodeSniffer?tab=contributing-ov-file#final-words

#### Discussion

There wasn't really any dissent, though several folks pointed out that for many trivial types of code, it's next to impossible to determine if an LLM wrote it or not.
The consensus was generally that we should add language to the contributor guide (and likely the PR template) that LLM-generated contributions likely cannot be submitted with sign-off attestation of ownership, and that any contribution made should be understandable and maintainable by the author and maintainers.
Aleksei noted that "understandable" requires effort by the maintainers to validate; Matthew and Rob countered that having this verbiage would allow maintainers to refuse obviously AI-generated code, as well as close issues if the discussion within the issue is clearly nonsense or generated.

#### Decisions

Matthew volunteered to draft verbiage for the contributor guide and PR template, and then submit it to the TSC to vote when ready.
