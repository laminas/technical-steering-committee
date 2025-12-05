# Minutes from the 2025-12-01 Laminas Technical Steering Committee Meeting

- When: 2025-12-01 at 19:00 UTC, until 20:08 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - James Titcumb
    - Julian Somesan
    - Luís Cobucci
    - Matthew Weier O'Phinney
    - Michał Bundyra

Quorum WAS NOT met (7 out of 16 members were present).

## Agenda

### Discussion around v3 of `laminas-session`

The [current open PR](https://github.com/laminas/laminas-session/pull/168#issuecomment-3576330083) in the branch `3.x` of `laminas-session`  raised some questions which can be clarified here.

1. Is the CSRF validator and Form element relevant any more? Can they both be deprecated and removed?
2. If not, should we be making a new library specifically for laminas-csrf to decouple `session` from `validator` and form from session

#### Discussion

Folks were generally in agreement that these actions should be taken, as they reduce dependencies for the main libraries, while providing a path to migrate for existing users. Julian initiated an async vote.

Aleksei noted that laminas-validator v3 already removed the CSRF validator, which means we would need to create the new package. There was some discussion whether or not we could consolidate the mechanisms between Laminas and Mezzio to avoid duplication; the consensus was "likely", but that the part that is useful is how the submitted token and original token are retrieved (http and session libraries, respectively).

### Enable `immutable` releases for libraries

Based on the [GitHub announcement](https://github.blog/changelog/2025-10-28-immutable-releases-are-now-generally-available/), we may want to enable immutable releases for all packages from now on. On both Mezzio and Laminas GitHub organisation.
It was discussed briefly several times in Slack, without a conclusion.
It is an easy step, can be enabled at Org level, and probably will become an industry standard.

#### Discussion

Again, general approval. Aleksei noted that you can also mark historical releases as immutable using the GitHub API, and recommended we do that. Julian initiated an async vote.

### Clarify the marketing message and use of domain `mezzio.org`

Several days ago it was a discussion on Slack which raised the problem about "what is what" in Laminas.

Quoting @ramsey:

> If I'm describing the relationship between Mezzio and Laminas to someone, is it appropriate to say "Mezzio is a Laminas project" or "Mezzio and Laminas are sister projects" or something else?"
> 
> In documentation, if I'm linking the word Mezzio to a canonical URL, it would be best to use docs.mezzio.dev or getlaminas.org. I note there's no "home" page for Mezzio; that appears to be the Laminas page (where it has the big "hero" section for Mezzio)

Since we have the domain `mezzio.org`, what if we move (or copy) everything related to Mezzio (including documentation) to this new domain? Mezzio is the main product of Laminas Project, and we may consider that it needs its own standalone presence and website. Currently, Mezzio documentation is waiting for a complete refactor so will be an opportunity to reconsider its location and structure. 

#### Discussion

Frank has previously suggested we use `mezzio.dev`, as we already own it, and have it redirecting to `docs.mezzio.dev`; we could just change it to not redirect and instead serve the site.

Julian owns the `mezzio.org` domain, and will transfer it to the Linux Foundation regardless. He feels that a `.dev` domain shouldn't be used for marketing. Others were not as convinced, but Aleksei pointed out that we have precedence (`getlaminas.org` being the project home). However, he also expressed a preference for `mezzio.dev` as the Mezzio home page. Julian further explained that `.dev` was a XAMPP usage pattern until it became a TLD, which is part of why he struggles to use it for websites. Aleksei noted that `.dev` has been a TLD for a decade now, which means anybody still doing that is likely having issues with DNS already.

Matthew proposed the following votes:

- Shall we have a dedicated marketing domain/website for Mezzio?

Followed by:

- What domain should we use for the Mezzio marketing website:
    - [mezzio.dev](http://mezzio.dev/)
    - [mezzio.org](http://mezzio.org/)
    - [getmezzio.org](http://getmezzio.org/)
    - None of the above
