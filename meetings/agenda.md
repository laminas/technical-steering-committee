# Next Technical Steering Committee Meeting Agenda

- Date: 2025-12-01
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Discussion around v3 of `laminas-session`

The [current open PR](https://github.com/laminas/laminas-session/pull/168#issuecomment-3576330083) in the branch `3.x` of `laminas-session`  raised some questions which can be clarified here.

1 - Is the CSRF validator and Form element relevant any more? Can they both be deprecated and removed?

2 - If not, should we be making a new library specifically for laminas-csrf to decouple `session` from `validator` and form from session

### Enable `immutable` releases for libraries

Based on the [GitHub announcement](https://github.blog/changelog/2025-10-28-immutable-releases-are-now-generally-available/), we may want to enable immutable releases for all packages from now on. On both Mezzio and Laminas GitHub organisation.
It was discussed briefly several times in Slack, without a conclusion.
It is an easy step, can be enabled at Org level, and probably will become an industry standard.

### Clarify the marketing message and use of domain `mezzio.org`

Several days ago it was a discussion on Slack which raised the problem about "what is what" in Laminas.
Quoting @ramsey
> If I'm describing the relationship between Mezzio and Laminas to someone, is it appropriate to say "Mezzio is a Laminas project" or "Mezzio and Laminas are sister projects" or something else?"

> In documentation, if I'm linking the word Mezzio to a canonical URL, it would be best to use docs.mezzio.dev or getlaminas.org. I note there's no "home" page for Mezzio; that appears to be the Laminas page (where it has the big "hero" section for Mezzio)

Since we have the domain `mezzio.org`, what if we move (or copy) everything related to Mezzio (including documentation) to this new domain ?
Mezzio is the main product of Laminas Project, and we may consider that it needs its own standalone presence and website.
Currently, Mezzio documentation is waiting for a complete refactor so will be an opportunity to reconsider its location and structure. 
