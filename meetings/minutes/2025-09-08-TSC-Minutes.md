# Minutes from the 2025-09-08 Laminas Technical Steering Committee Meeting

- When: 2025-09-08 at 19:00 UTC, until 20:19 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Aleksei Khudiakov
    - Abdul Malik Ikhsan
    - Frank Brückner
    - George Steel
    - Julian Somesan
    - Matthew Weier O'Phinney
    - Michał Bundyra

Quorum WAS NOT met (7 out of 16 members were present).

## Agenda

### PHP Download & Installation Instructions

The topic discusses whether Laminas should be mentioned on the [PHP downloads](https://www.php.net/downloads.php) page, similar to [Symfony Setup](https://symfony.com/doc/current/setup.html).
Matthew mentioned this [tutorial](https://docs.mezzio.dev/mezzio/v3/getting-started/quick-start/), but it implies that PHP is already installed.
Julian intends to append to the page: the installation of PHP, choosing a PHP version, setting up extensions, and installing composer.

#### Discussion

George and Rob were in favor of extending the documentation, which can lead to smoother onboarding, with guides on how to start on a new project.
Julian mentioned there are already 2 articles in the Mezzio 101 series and more can be added.
The members agreed that the exposure on the php.net site would be beneficial for the Laminas Project.

#### Decisions

Julian will add the relevant paragraphs to the quick start page.
Then a PR will be created on php.net.

### Private repo for private Laminas project related items

For security and practical reasons, several logins and source files should be kept in a private repository:

- source files e.g. for current Laminas design (only .svg is available)
- logins e.g. for Mastodon @getlaminas account

#### Discussion

Matthew mentioned he has been using Enpass and KeePassX for password management.
He believed that a central password vault like 1Password is required and, once set up, should be shared between maintainers.

Matthew considered that a private repo would be free, but ultimately, not needed.

#### Decisions

The various logins should be shared between the maintainers to ensure redundancy.
The members opted for [1Password](https://1password.com/) and started messaging the people who set up the various social accounts.

They also decided that a private repository is not needed, since it's ok to keep the logo source files public.

### New header for Mastodon and LinkedIn

Should references to Zend Framework be removed from the getlaminas.org tagline?

#### Discussion

The discussion started with the tagline 'A community supported, open source continuation of Zend Framework'.
Matthew and Julian agreed that awareness of ZF is still great in the PHP community.
Conversely, Aleksei believed that that the link between Laminas and ZF is not providing any benefits.

The members considered ideas for a new tagline.

#### Decisions

The issue that mentioned this topic was converted to a [discussion](https://github.com/laminas/getlaminas.org/discussions/325) for brainstorming new tagline ideas to be voted on in a future meeting.

### New official logos

During the previous month, the TSC members chose the main Mezzio logo.
They now needed to decide on the text below the logo:

- microframework
- by Laminas project
- by Laminas
- powered by Laminas Project

#### Discussion

Matthew, Aleksei and George opted for 'by Laminas', since the other options are not a good match for Mezzio.

#### Decisions

Since there was no quorum, a poll was created to vote on the variant and passed with most votes in favor of 'by Laminas'.
