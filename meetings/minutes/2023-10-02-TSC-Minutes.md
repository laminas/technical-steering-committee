# Minutes from the 2023-10-02 Laminas Technical Steering Committee Meeting

- When: 2023-10-02 at 19:00 UTC, until HH:mm UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - Andreas Heigl
    - George Steel
    - Luís Cobucci
    - Marco Pivetta
    - Matthew Weier O'Phinney
    - Rob Allen

Quorum WAS met (8 out of 15 members were present).

## Agenda

### PHP 8.3 compatibility

Lets talk about PHP 8.3 and discuss how to accomplish the PHP update this year. RC1 of PHP 8.3 will land on 2023-08-31.
We may need to wait until there is at least RC1 available via sury so that we can add it to the CI container - or we temporarily use shivammathur again.

#### Matrix & Container action

Another thing we might want to CI container and Matrix in action in the same repository might help.

Do we actually need a "container action"? Matrix action should suffice from a projects PoV, there should be no project using the container action without the matrix action as that would reuqire projects to actually write a JSON within the workflow file to suit the action requirement (i.e. passing the JOB JSON).

#### Projects within `laminas`/`mezzio`/`laminas-api-tools`

_First of all, is there a plan for API Tools? Is it meant to be abandoned?_

We need projects per Org to keep track of PHP 8.3 migration progress. Do we want to tackle this the same way as the last updates:
- create project
- run a shell script to auto generate PHP 8.3 compatibility issues while attachingn them to the project

#### Renovate

What about renovate? Renovate will help us to migrate to PHP 8.3 as far as I understood correct.
Is it possible to tell renovate to actually add PRs created by renovate to the PHP 8.3 projects (once created) mentioned above?

#### Discussion

The container and matrix are already ready, so the main discussion is whether or not Renovate can be configured to use the RCs in order to trigger pull requests.

Matthew W argued that allowing builds against RCS gives us more breathing room, allowing us to do releases on critical packages early, so we don't have to field as many upgrade requests when the GA release happens.
Aleksei had reservations about allowing RC versions in the package dependencies.
Marco expressed support for allowing them, with agreement from Andreas.

#### Decision

Aleksei is going to enable the RCs for Renovate.

### Migrate from X/Twitter to Mastodon

We can no longer automate posting to Twitter, er, X, or Xitter, whatever, due to changes in the pricing model for the API.
This means any posting we do MUST be done manually, from Twitter or Tweetdeck, and, further, sharing credentials is becoming increasingly difficult.
On top of that, continued usage of the platform is de facto endorsement of a far-right, fascist agenda promoted by the owner of the platform.

Matthew W suggests:

- We immediately disable and/or delete our account on Xitter.
- We consider creating an account on phpc.social.
- We audit what automations we had in place for Twitter (e.g. release announcements, Slack integration) and determine what, if any, we want to move to the new account.

#### Discussion

Everybody was in favor of this.
The main discussion was whether or not to spin up our own instance (e.g. laminas.social) to host the bot.
Most agreed that it's outside of our domain to host it ourselves, and doesn't make a lot of sense for a single, mostly bot, account.

There was also a question about reserving a handle on BlueSky.
We generally agreed that we should, but likely will not post there immediately.

#### Decision

We will immediately register a handle on phpc.social; Andreas stepped up to do so.
Main things at this point are (a) what email address to use for registration, and (b) how to share credentials between TSC members once registered.
These will be determined soon; Andreas and Matthew will coordinate.
