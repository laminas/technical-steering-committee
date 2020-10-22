# Next Technical Steering Committee Meeting Agenda

- Date: 2020-11-02
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

### RFCs - discuss directly on GitHub?

As [noted by the user on the laminas slack](https://laminas.slack.com/archives/C4QBQUEG5/p1602604527127400), our current issue template suggests that
new features/RFCs should be posted to the forums for discussion.

That is quite inefficient, since:

 * the amount of users following the forum is a fraction of the users following our repositories
 * it is one more step for people to contribute

It could be a good idea to just endorse opening issues as "feature request" or "RFC" instead, since all the Laminas TSC members and community members
are quite familiar with PR/issue tooling of GitHub.

### Github Actions instead of Travis-CI?

Github Actions has been, so far, much faster and efficient to set up in repositories all over github.

While Travis-CI is certainly a good platform that has served us well for many many years, having the ability to create our own github actions may simplify
the CI setup for most our repositories.

The proposal is to:

 * Find an optimal "baseline" Github Actions workflow that we'd like to use
 * Investigate whether there is a way to unify most CI workflows (rather than maintaining them in each repository)
 * Move current Travis-CI configuration to Github Actions workflows
 * Sunset Travis-CI configuration and disable it on the various repositories
