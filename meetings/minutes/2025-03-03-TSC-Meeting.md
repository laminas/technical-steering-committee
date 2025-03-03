# Minutes from the 2025-02-03 Laminas Technical Steering Committee Meeting

- When: 2025-03-03 at 19:00 UTC, until 20:06 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - Frank Brückner
    - George Steel
    - Julian Somesan
    - Matthew Weier O'Phinney

Quorum WAS NOT met (6 out of 16 members were present).

## Agenda

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

#### Discussion

Matthew asked what the issue is exactly: lack of reviews, conflicting ideas during review, or something else? Julian responded that it's the lack of reviews.

George and Julian both noted that releasing the website is not nearly the same risk as releasing code packages; we can iterate on the design without it having a tangible impact on consumers in most instances.

Julian indicated that the bulk of the PRs are coming from his team. Matthew suggested that Julian should feel empowered to merge their PRs, and then ping the TSC membership to review any he submits himself. This was met with general approval, but Julian pointed out that for the major PRs (redesign, ecosystem pages), we'd need a TSC vote.

### New design

The PR is here: https://github.com/laminas/getlaminas.org/pull/260
The preview is here: https://preview-1-hy2vwsq-2ja7ciew2nbkm.us-2.platformsh.site/
It is still work in progress, but we can discuss about the general design look and feel. 
We will have a future page for **Mezzio 101** tutorials and materials.

#### Discussion

Matthew asked if there was an action item, or if this was a status update; Julian replied that it's a status update.

Julian's main question was whether to link to the frameworks/projects that use Laminas components, or if we should get permission first. General consensus was that we can go ahead and link, and if they have a problem with it, we can remove the links.

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

#### Discussion

Aleksei opens by saying "I agree. Shove the mvc into the far corner," which was met with laughter and enthusiasm.

Julian points out that the original selling point of Laminas was as a continuation of Zend Framework", but that the project has already shifted its focus. Additionally, he notes we should point to the future, not the past of the project.

(That said, he also notes that MVC is still quite popular, and we shouldn't completely disappear it!)

The new redesign does not have link to the MVC project on the homepage, and Julian and his team have started a series of "101" articles and tutorials that focus on Mezzio, to help newcomers become successful with middleware. His goal is that Mezzio will be "the product" that people see when they come to the Laminas website.

Aleksei suggests we stop funneling people to the MVC project and docs, and maybe even segregate components into groups that can be used standalone versus those that only work with the MVC. Julian indicates that this is part of the planning he is working on.

While there is general consensus, Julian will initiate an async vote to validate.

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

#### Discussion

Matthew suggests we need a usage option to indicate a "library" or "component" that can be used standalone, citing components like Tag and Feed and Paginator as examples. Aleksei suggests that categories should allow freeform words, similar to how keywords work in Composer; Julian says we can then make suggestions on categories, but not enforce them.

Aleksei then asked why we need both categories and keywords. Julian explained it's to allow differentiating projects (which will be installed _on top of_ a framework), middleware (which can be installed in a pipeline), and libraries (which can be used standalone). Aleksei clarified further to application, tooling, and library.

The final clarification:

- Usage: application, tooling, library
- Categories: freeform keywords
