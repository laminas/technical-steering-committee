# Next Technical Steering Committee Meeting Agenda

- Date: 2023-10-02
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

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

### Migrate from X/Twitter to Mastodon

We can no longer automate posting to Twitter, er, X, or Xitter, whatever, due to changes in the pricing model for the API.
This means any posting we do MUST be done manually, from Twitter or Tweetdeck, and, further, sharing credentials is becoming increasingly difficult.
On top of that, continued usage of the platform is de facto endorsement of a far-right, fascist agenda promoted by the owner of the platform.

Matthew W suggests:

- We immediately disable and/or delete our account on Xitter.
- We consider creating an account on phpc.social.
- We audit what automations we had in place for Twitter (e.g. release announcements, Slack integration) and determine what, if any, we want to move to the new account.
