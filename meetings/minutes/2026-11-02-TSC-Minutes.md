# Minutes from the 2026-11-02 Laminas Technical Steering Committee Meeting

- When: 2026-11-02 at 19:00 UTC, until 19:58 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Frank Brückner
    - George Steel
    - James Titcumb
    - Julian Somesan
    - Luís Cobucci
    - Marco Pivetta
    - Matthew Weier O'Phinney
    - Rob Allen

Quorum WAS met (8 out of 16 members were present).

## Agenda

### Security Reports

Though there were no new items on the agenda, Matthew mentioned the large number of new security reports and that he would have no time to triage and patch them, only provide reviews.

#### Discussion

Frank observed that several new security-related pull requests (PRs) were submitted and that they were created with AI assistance.
James remarked that the PRs are likely genuine, but they still need to be triaged, and that he would have preferred them to be private.

Julian linked one security issue in a private fork already approved by Aleksei, asking how to handle it.
Matthew advised developing a patch on the oldest branch with the oldest supported PHP version, then having it approved by members of the TSC and released for each branch after that.

Julian offered to triage and patch the security issues and submit them for review to other members of the TSC.
Several other members in the call were ok with Julian's proposal.

#### Decisions

Julian and his team will be handling the triage and patching of security issues.
He would then submit the patches for review to other members of the TSC.
Finally, the approved patches will be merged into the affected branches.
