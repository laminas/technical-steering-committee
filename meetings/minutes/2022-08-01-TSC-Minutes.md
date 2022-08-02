# Minutes from the 2022-08-01 Laminas Technical Steering Committee Meeting

- When: 2022-08-01 at 19:00 UTC, until 20:11 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Aleksei Khudiakov
  - Andreas Heigl (left at 20:00 UTC)
  - Frank Brückner
  - Gary Lockett
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Setter (left at 20:00 UTC)
  - Matthew Weier O'Phinney
  - Maximilian Bösing
  - Michał Bundyra

Quorum WAS met (11 out of 16 members were present).

## Agenda

### Short(!) feedback on open issues:

- https://github.com/laminas/technical-steering-committee/issues/69 - Linux Foundation has been able to set up email-aliases so at this point in time there's no need to switch email-providers.
- https://github.com/laminas/technical-steering-committee/issues/71 - Adding branch protection to all repositories - Is this something that we want to do? If so: let's put that onto the agenda for the september-meeting and invite @Slamdunk for that.
- https://github.com/laminas/technical-steering-committee/issues/68 - @mwop wrote down notes and tasks as follow up to marking packages as security only. Are these notes still up-to-date? Or can this be closed by now?
- https://github.com/laminas/technical-steering-committee/issues/6 / https://github.com/laminas/laminas-mvc/issues/41 - Some links to LaminasSkeletonModules are/were broken: what is the actual state here? Docs are vital to the projects success and broken tutorials are worse than no tutorials at all. Do we need to improve here?

#### Discussion

Matthew W indicated that 68 and 69 can be closed; Andreas went off and closed them immediately.

Aleksei indicated that the ZendSkeletonModule was never ported to Laminas, as we made a decision not to.
What is needed is to add a CLI action for creating a module, and then these can be closed.
Matthew W indicated that the tool would just need to create a directory structure (based on layout chosen), create a `Module` class file in that tree, and then register it with the `config/modules.config.php` file.
He asked Aleksei to create a feature request on the releveant repository and assign him to it so we can complete it.

For item 71, Matthew W was not sure who was rolling that out originally.
Aleksei volunteered to audit and make sure we have branch protections on all repositories.

### Laminas Continuous Integration Actions

As of today, we do maintain `laminas-ci-matrix-action` and `laminas-continuous-integration-action` in separate repositories.
Every year, when a new PHP version comes out, both repositories needs changes so that the matrix will create jobs for the new PHP version and the action uses that new version when running jobs.

Since that is actually the main job of both actions (to be in sync when it comes to PHP versions), [Marco](https://github.com/Ocramius) suggested to merge both actions to the same repository so we can keep releases in sync.

[Max](https://github.com/boesing) is actually working on some kind of `before_script` logic which allows projects and the CI matrix action to provide commands which are executed before every command run.
This has to be first implemented in the `laminas-continuous-integration-action` before it can be added to the `laminas-ci-matrix-action` (or we need at least a synchronized release).

Lets gather some ideas on how this could look as we have to create dedicated releases per action. Having projects to update their workflows because we create a monorepo should be avoided.

#### Discussion

The main gist of the discussion was around whether we should move the containers into the action repos, or vice versa.
Matthew W noted that moving the actions into the containers would mean anybody consuming the actions would need to change their workflows to refer to the new actions, as actions are tied to repository names.
Moving the containers into the actions would mean we could archive the old repos, but users could still use those containers if they were using them separately from the actions.

Max asked how this would affect tags.
Matthew W suggested that we bump the minor version to 1 more than the latest minor version on either repository, giving the example that if the container were at 1.32, and the action at 1.27, we'd do a new release of 1.33.
This would ensure the tag is unique.
And since the workflow and action pin to a tag based on major version (e.g. `:1`), then that version will get picked up.

#### Decision

We voted in favor of moving the container code and packages into the action repositories, allowing them to evolve together.
Max will take point on this.

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

#### Discussion

Matthew W apologized for opening this can of worms, and suggested we focus only on the GreetBot replacement.
When pressed, he suggested that we save discussion of Slack alternatives to after we've brainstormed what we need out of a chat solution, and then done research to determine what options there are, and how each does or does not address those needs.

(This did not stop the inevitable MS Teams bashing, nor the recommendations of replacements!)

#### Decision

We decided to move forward with CommonRoom for the time being.

### Coding style new major release

In the laminas/laminas-coding-standard#75 there are BC breaks in the slevomat ruleset dependency. A rule rename affected us and there are a few more breaks, which do not affect us. Since we (should) lock to minor versions `~2.3.0`, it does not make a difference if we release 2.4 or 3.0 as we (or renovate) need to update all packages either way.

To prevent upgrade issues and supporting multiple versions, the preference would be create a 3.0 release.

#### Discussion

The impetus for this is two items:

- We've observed rulesets change/rename in minor versions, which can cause breakage in our CI.
- CodeSniffer itself has had breakage even in patch versions (though, as Luís notes, it's rare... but when it happens, it can be painful).

Matthew W suggested that we probably should have a different rule for laminas-coding-standard with regard to new major releases, as any addition or rule change is essentially a BC break; as such, new major releases should be normalized for the tool.
This was met with agreement.

Max and Geert wondered if we should be pinning the _dependencies_ for laminas-coding-standard to minor versions as well, to prevent breakage.
Geert suggested going so far as to pin to patch versions, as he's encountered BC breaks/bugs between patch versions on more than one occasion.

#### Decision

We decided to roll a new major, and start pinning dependencies to minor releases to prevent future headaches.
We will pin phpcs itself to patch versions.

### Commercial Vendor Program application

We have received our first outside application:

```text
twitter:  @dotkernel
Laminas slack username: arhimede

I am the CTO of the company Apidemia   
https://www.apidemia.com/

We develop our own collection of applications and packages on top of Mezzio and Laminas 
https://www.dotkernel.com/

We have been  using  Zend Framework  since the very beginning,.
On  a  side note, we are keeping up and running the last PEAR ZF 1 channel 
http://pear.dotkernel.com/

Since our main business line is providing Consulting and Development service using Mezzio//Laminas, I
think that we can benefit from being listed on the Commercial Vendor Program page.
```

Per our application process, the next step is to vote on the application; if approved, they will need to provide proof of donation before we list them.

#### Discussion

Gary wondered if we should be doing some due diligence before we come to a vote, and Matthew W pointed out this was always an option, and that we could do an offline vote.
Gary clarified later that we should reach out to the company to ensure the donation comes from them, and that we have their permission to add the association; Matthew pointed out that this is why we have them send their donation receipt to us.

However, Matthew W also noted that DotKernel has been active in the ecosystem both before and after the migration, and has communicated with Julian (the applicant contact) a number of times within the Slack.
Aleksei remembered the project being very active in the old ZF IRC channels as well.
Marco noted that the process is mainly to protect us from spammers/scammers, and that the email, along with the fact multiple folks on the TSC knew them, was "good to go".

#### Decision

We voted to accept DotKernel as our first outside member of the Commercial Vendor Program.
Matthew W will work with them to ensure the donation is made, and to get their logo and blurb for the website.

## Next Meeting

The next meeting will be held Monday, September 12, 2022, at 19:00 UTC.
(Meeting is delayed by a week as September 5 is Labor Day in the US.)
