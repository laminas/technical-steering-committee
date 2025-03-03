# Next Technical Steering Committee Meeting Agenda

- Date: 2025-03-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### How to speed up the branding and marketing efforts

The subject was discussed in October 2024 TSC meeting in conjunction with the Marketing and Branding committee, but the progress is slow.
Right now, there are several open PR's and we do not have enough preview branches to keep all of them open.
There is a large gap between new published articles since the January TSC meeting.
We have a couple of articles on the pipeline since mind-February, so I would kindly suggest to take advantage of the time and developer hours spent on them.
Julian Somesan is proposing to improve the PR workflow on *websites* group and is asking for permission to merge PR's even if those PR's are open by Apidemia's dev team.

PR with articles open :

- https://github.com/laminas/getlaminas.org/pull/251
- https://github.com/laminas/getlaminas.org/pull/250

PR related to opengraph: https://github.com/laminas/getlaminas.org/pull/259

### New design

The PR is here: https://github.com/laminas/getlaminas.org/pull/260
We will have a future page for **Mezzio 101** tutorials and materials

### Repo for tutorials

The series of **Mezzio 101** related articles in the blog may need some code repositories with tutorials.
Can we list them under Laminas or Mezzio organisation ?

### Change communication and focus on Mezzio and middlewares

Right now, the principle and current communication is aimed at **Laminas Project and sub-projects**.
Julian Somesan is proposing to change that into: **Laminas and Mezzio component and middleware microframework** in order to give more emphasis to Mezzio, middlewares, PSR-15, and so on.
We do not abandon laminas-mvc, only shift it a bit from the frontline.
Current tagline:
> Laminas Project, the enterprise-ready PHP Framework and components
> An open-source, community-driven successor to Zend Framework

Proposed new tagline:
> Laminas & Mezzio: Enterprise-ready, Open Source PHP components and middleware microframework.
> A community-supported, open source continuation of Zend Framework.

This decision will influence both the new design of the main website getlaminas.org, and the secondary websites.

### Criteria for including in Ecosystem page

Below is listed a more detailed description of the Ecosystem page.
Current questions that we should talk about are:

- which should be the **categories**? (other then `skeleton` `integration` `tool`)
- what other options we should have for **usage** ? (other then `mezzio` `mvc`)

Current behaviour requires packages to be at least **listed** on packagist.com.
If the requirement shifts to requiring to be **installable** via composer, how should we handle `project` type packages which may require cloning instead of installing (i.e. `dotkernel/api` strongly recommends cloning)?

Adding packages is done by editing the `ecosystem-packages.json` file.
At the moment there's no limit on how many packages can be added at once.

The process is not automated, with users having to create pull requests that must be reviewed by maintainers.

Abandoned packages are skipped by default - should this still be the case?

Removing packages is currently done by deleting the entry and submitting a PR, with no other steps required.
A `--force-rebuild` flag is also available for the command (and as a platform.sh runtime operation) to regenerate the database file from scratch if necessary.

On PR and push, a separate GitHub action runs to check if the json file is valid, not empty, and that all the entries contain the mandatory keys.

Users adding packages **must** include the following keys:

- `packagistUrl`: mandatory, the information is collected by calling the Packagist API using this url
- keywords: allows the user to define keywords to use as filters in the interface
    - currently no limit set on either keyword length or number of keywords
    - users can skip adding keywords by leaving the array empty
- `usage` (`mezzio`, `mvc`): a mandatory single choice 'flag' that indicates a package's intended use
    - any given value that does not match an option will cause the package to be skipped
- `category`: mandatory, single choice field with the following values:
    - `skeleton` -> usually 'project' type packages, providing an application base to build upon (e.g. mezzio-skeleton, which also inspired the name)
    - `integration` -> packages that are based on, or extend others to bring further functionality (e.g. dot-sessionm extending laminas-session)
    - `tool` -> standalone package that brings own functionality (e.g. laminas-filter)
    - any given value that does not match an option will cause the package to be skipped

- homepage: allows users to set a custom url for the homepage button in the interface
    - if nothing is set by the user, the homepage is set from packagist if any is available, with the button skipped if none there as well

