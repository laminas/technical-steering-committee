# Minutes from the 2025-06-02 Laminas Technical Steering Committee Meeting

- When: 2025-06-02 at 19:00 UTC, until 19:49 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Frank Brückner
    - George Steel
    - Julian Somesan
    - Matthew Weier O'Phinney
    - Michał Bundyra
    - Rob Allen

Quorum WAS NOT met (6 out of 16 members were present); all votes were initiated asynchronously, with results to publish later.

## Agenda

### Maintainer Nomination

[@gsteel](https://github.com/gsteel/) would like to nominate  Richard McHale ([@ramchale](https://github.com/ramchale)) as a maintainer of `laminas-filter`, `laminas-inputfilter` and `laminas-validator`.

Richard has provided a number of high quality contributions to laminas-filter that were instrumental in getting v3 over the finish line, and has expressed his interest in continuing to help triage issues, review PRs and perform maintenance duties as a member of the team.

#### Discussion

Matthew started the discussion by indicating he's been impressed with Richard's PRs to date.
George pointed out again how much help Richard was during the laminas-filter v3 push.

Matthew opened the vote.

### Place for Discussion

At the moment we are using different channels for different discussions. 
The Discourse forum is used for user questions, and I would not like to change that at this point.
But for technical discussions, I would like to have a single place where we can discuss all topics.

We have issues and PRs on GitHub, but they are not the best place for discussions, especially when it comes to future developments.
And we have Slack, but it is more a chat tool, and not the best place for technical discussions either, because it is not persistent and not topic-related.
Then we have the discussion feature open on GitHub, but only for some repositories.
For example:

- https://github.com/laminas/laminas-cli/discussions
- https://github.com/laminas/laminas-view/discussions
- https://github.com/laminas/technical-steering-committee/discussions

But I would not open the discussions on all repositories.
So the question is: do we want to have a single place for discussions, and if yes, which one?
On a specific repository or on for the whole organization?
Or there are other options/ideas?

#### Discussion

George immediately recommended we open GitHub Discussions at the org-level.
Matthew asked if this should happen just on the Laminas org, or also on the Mezzio org.
The suggestion in the end is that we open them on both, but:

- For the Mezzio org, we would pin a message directing folks to use the Laminas Discussions instance.
  Any topics started there would get a reply asking the contributor to recreate it on the Laminas Discussions instance, and the topic would be immediately closed.
- For the Laminas Discussions instance, we would pin a message indicating that these are for technical/development discussions only, and point people to our Discourse instance for community help.

George volunteered to create the pinned messages if the measure passes.

A vote was opened.

### Push live the getlaminas.org new design

[The preview is here](https://preview-1-hy2vwsq-2ja7ciew2nbkm.us-2.platformsh.site/)

There are some details to fix here and there, and maybe new pages to be created or update, but we may push it live as is now.

We can fix details later, it is still work in progress, but at least we can show progress, and reflect the changes in focus of the project.

#### Discussion

George suggested we just go ahead and publish; we can fix iteratively once we have.
Several others chimed in with their agreement.
Frank, however, felt that there are too many problems and errors, both big and small, to go live.

While we opened a vote, Rob also suggested that we may want to develop an odd-numbered sub-committee for the website.
Several folks agreed that this would be a way to prevent deadlock between contributors.
Matthew indicated he will bring this up with the TSC for discussion between now and the next meeting.
