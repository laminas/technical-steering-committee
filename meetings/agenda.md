# Next Technical Steering Committee Meeting Agenda

- Date: 2022-08-01
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Short(!) feedback on open issues:
* https://github.com/laminas/technical-steering-committee/issues/69 - Linux Foundation has been able to set up email-aliases so at this point in time there's no need to switch email-providers.
* https://github.com/laminas/technical-steering-committee/issues/71 - Adding branch protection to all repositories - Is this something that we want to do? If so: let's put that onto the agenda for the september-meeting and invite @Slamdunk for that.
* https://github.com/laminas/technical-steering-committee/issues/68 - @mwop wrote down notes and tasks as follow up to marking packages as security only. Are these notes still up-to-date? Or can this be closed by now?
* https://github.com/laminas/technical-steering-committee/issues/6 / https://github.com/laminas/laminas-mvc/issues/41 - Some links to LaminasSkeletonModules are/were broken: what is the actual state here? Docs are vital to the projects success and broken tutorials are worse than no tutorials at all. Do we need to improve here?

### Laminas Continuous Integration Actions

As of today, we do maintain `laminas-ci-matrix-action` and `laminas-continuous-integration-action` in separate repositories.
Every year, when a new PHP version comes out, both repositories needs changes so that the matrix will create jobs for the new PHP version and the action uses that new version when running jobs.

Since that is actually the main job of both actions (to be in sync when it comes to PHP versions), [Marco](https://github.com/Ocramius) suggested to merge both actions to the same repository so we can keep releases in sync.

[Max](https://github.com/boesing) is actually working on some kind of `before_script` logic which allows projects and the CI matrix action to provide commands which are executed before every command run.
This has to be first implemented in the `laminas-continuous-integration-action` before it can be added to the `laminas-ci-matrix-action` (or we need at least a synchronized release).

Lets gather some ideas on how this could look as we have to create dedicated releases per action. Having projects to update their workflows because we create a monorepo should be avoided.

### Slack and Greetbot service changes

- Submitted by [Matthew Weier O'Phinney](https://github.com/weierophinney)

We've been using Slack for years, and it works fine.
The main rationale for using it over other solutions has been:

- Ease of use over older protocols like IRC.
- Famililarity in the ecosystem.
- Works via standard web ports (specifically 443), preventing issues with corporate firewalls.

Along with Slack, we've been using a service called Greetbot since we renamed to Laminas.
Greetbot messages a user after they've first registered, providing them with a welcome message, and a list of handy links (documentation, website, forums, etc.)

Today, both services are having some significant changes.

- Greetbot ends service mid-August.
- Slack has changed from having a maximum allowed history **size** (10k messages) for organizations on the free plan to a maximum allowed history **duration** (90 days).
  Currently, it appears our messages expire somewhere in the 4-6 month range; **as of today, anything older than 90 days expires.**

At the time we chose Slack, a number of folks argued we should use Discord, but quite a few folks argued against it indicating their place of business restricted access to it as it was considered a "gaming" site.
However, that landscape has changed dramatically over the years; in fact, even Google is [using Discord as the primary communication forum for Carbon](https://thenewstack.io/google-launches-carbon-an-experimental-replacement-for-c/) (its recently announced C++ alternative/succesor).
As a result, it's increasingly rare to have bans on Discord within companies, particularly those doing software development.

Two key reasons for us to consider moving to Discord: there are no message limits, and it offers welcome message templates by default already, without requiring any additional services.
Additionally, it has far better moderation tools; in fact, we can even require users to verify they've read our code of conduct before they can complete registration.
It does, however, miss a few other features that Slack gives us (threading and reminders in particular).

I see a few different routes we could go:

- Keep Slack.
  If we do, we'll need to remember that anything older than 90 days disappears.
  We'll also need a Greetbot replacement (best one I've found with a free plan is [CommonRoom](https://www.commonroom.io/pricing/)).
- Migrate to Discord.
  If we do this, we'll need to setup our welcome message templates (I already have them from Greetbot), and:
  - Update our GitHub webhook on laminas.dev to talk to Discord.
  - Somehow migrate our users to the new system. (We'd need a plan.)

I'd like to begin discussions, with a goal of, at the minimum, determining how we will address welcome messages when Greetbot closes doors.
