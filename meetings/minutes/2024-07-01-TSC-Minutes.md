# Minutes from the 2024-07-01 Laminas Technical Steering Committee Meeting

- When: 2024-07-01 at 19:00 UTC, until HH:MM UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brückner
  - George Steel
  - James Titcumb
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Michał Bundyra
  - Rob Allen

Quorum WAS met (9 out of 15 members were present).

## Agenda

### Create Media Kit

- create new logos or improve the current ones , for Laminas and Mezzio
- svg format, various sizes and color
- create few wallpapers
- stickers from stickermule
- banners and badges: "powered by Laminas" , or "powered by Mezzio"
- official banner/seal for  "Official Laminas Commercial Vendor"
- any other ideas related to marketing materials
  
Responsible: Dotkernel organisation

Good to have it by: July 2024 TSC meeting

Where: a Media Kit page on getlaminas.org website

#### Discussion

We agreed that a media kit would be good, and Matthew noted that we have ample funds for things like stickers.
Julian Somesan indicated he will be paying for a brand designer out-of-pocket, and will have Frank involved in those decisions.


### getlaminas.org website update

We need approval for:

- https://github.com/laminas/getlaminas.org/issues/162
- https://github.com/orgs/laminas/projects/23/views/1

Dotkernel organisation want to be involved in this, with Frank Brückner @froschdesign as project lead.

The purpose is to have it ready on a new staging location, by July TSC meeting, for final approval.

#### Discussion

Frank is already collaborating with Julian on these PRs, and tasks are in hand already.

### OSS status for packages, and status page

For each package, add a file OSSMETADATA, with possible values:

- osslifecycle=active
- osslifecycle=maintenance
- osslifecycle=archived

and add the badge to readme file

Example:  ![OSS Lifecycle](https://img.shields.io/osslifecycle/dotkernel/api)

> #### Note
>
> Unfortunately, for this solution to be in effect, it needs a new release for each package.

Once complete, create a status page; [See this pull request](https://github.com/laminas/technical-steering-committee/pull/175).

For each Github namespaces: laminas-api-tools, laminas, mezzio, and for each package in the namespace.

List all packages and the badge for each, with its OSS status: active, maintenance, archived.

#### Discussion

Several folks noted that the idea is not to add a badge to the README, but instead set a custom property on each repository (custom properties are a new-ish feature of GitHub).
During discussion, it emerged that these are already created at the organization level, so now we need to set the values on each repository.
From there, we can use the GitHub API to create the status page.

Frank noted that defining the properties was the easy part; setting the values is the hard part.
George asked if we can set organization defaults; if so, we could just update the few that differ.
Frank pointed to some docs that validate that this is possible, and each of Eric Richer and Julian Somesan indicated they've done exactly this for organizations they control as well.

George volunteered to setup the organization-level defaults, and Matthew volunteered to setup the "exceptions" in each org.

### Extract Laminas Translator Interface to a new component

Introduce a new package `laminas-translator` that contains only the `LaminasTranslator` interface. Release 2 versions, v1.0 without native types and v2.0 with native types, i.e.

I've created a repository containing the proposed interface here: https://github.com/gsteel/laminas-translator that is hopefully ready to release.

```php
namespace Laminas\Translator;

interface Translator
{
    /**
     * Translate a message.
     */
    public function translate(
        string $message,
        string $textDomain = 'default',
        string|null $locale = null,
    ): string;

    /**
     * Translate a plural message.
     */
    public function translatePlural(
        string $singular,
        string $plural,
        int $number,
        string $textDomain = 'default',
        string|null $locale = null
    ): string;
}
```

Implement this interface in `laminas-i18n` so that all other components that consume a translator can rely on the interface without depending on `laminas-i18n` - then, hopefully, we'll have an easier time upgrading to service manager v4 in those components.

#### Decision

There was no discussion, and the measure passed unanimously.

### Vote on the nomination of Julian Somesan as TSC member

@weierophinney has nominated [Julian Somesan (@arhimede)](https://github.com/arhimede) as the newest member of the TSC. The [RFC](https://github.com/laminas/technical-steering-committee/issues/177) has attracted positive support and as per [processes](https://github.com/laminas/technical-steering-committee/blob/main/processes/VOTING.md), a vote must be conducted to approve his appointment.

#### Decision

Julian Somesan was unanimously accepted as our newest TSC member!

### Laminas Bus Factor

Recently, 3 of the most skilled, knowledgeable and senior members of the TSC have signalled their intent to either scale back or withdraw from opensource. Without these TSC members, Laminas and Mezzio would be left with vanishingly small pool of maintainers, many of which have little of their own personal time to work on the projects.

Of the 17 members of the TSC, at least 4 of these could be considered inactive. Typically, there are around 9 members at monthly meetings; with 3 further withdrawals, and assuming current attendance levels, despite the huge loss of expertise, we would likely not have quorum at any future meetings.

The time it takes for PRs from existing members and contributors to get reviewed and merged is, in my subjective opinion, increasing. By no means should this be considered criticism of individual members - we are all people with lives to lead and personal responsibilities.

The question is what can be done to improve the situation?

Here are a handful of ideas that can hopefully be used as talking points at the next meeting:

- use accrued Laminas funds to pay for an existing member to spend time on Laminas
- consider ways to reach and recruit new maintainers
- remove members from the TSC that no longer wish to participate in order to make quorum easier to reach
- ask for commitments from existing members to perform maintenance duties for a small amount of time at regular intervals. For example, perhaps each member could commit to 2 hours per week/month _(at a convenient time)_ to dedicate to the projects, using that time to review patches, make CI green, whatever…
- survey existing members for nominations of new maintainers

As someone who uses Laminas/Mezzio in client work, I have a vested interest in seeing the components continue to evolve and improve - and I believe the projects are solid and viable alternatives to the other major frameworks. It would be a shame to witness the slow death of the projects…

#### Discussion

Primarily, the discussion gravitated to having us do more efforts around branding and marketing.
Julian indicated again that this is something he is already working on, and is happy to do.

George suggested we advertise for maintainers in the README of each repository.
This was met with general enthusiasm.
Rob asked if we have process docs, and Matthew indicated we do.
Joey Smith pointed out that for many, they may be a bit difficult, but that if we can mentor new maintainers, that will help.
Marco and others pointed out that this is something we can absolutely help with as TSC members.

Eric Richer pointed out that we may need to look into creating "admin" roles for non-dev work, such as setting custom props, preparing the agenda, taking minutes, etc.
These would not need to be performed by TSC members.

### Licensing

The current state of open source is such that developers provide their time and expertise contributing to projects for no financial reward, whilst corporations reap the benefits by selling software and services built from those components for profit.

One way to redress this imbalance is via licensing - deny profit making enterprise access to software unless they pay for it.

- Is a discussion around re-licensing Laminas and Mezzio components worth having?
- Are there any existing licenses that could be adopted to improve outside investment?
- Could we use Laminas funds to pay for decent legal advice?
- Is potential non-use/reduction in use a concern?
- Would re-licensing be compatible with any constraints placed on us by the Linux Foundation?

#### Discussion

Matthew notes that the Linux Foundation already gives us access to legal advice.
However, he also notes that he's not sure how a license change might affect our ability to stay with the LF.

Marco notes that he believes that software lived in 3 eras:

- Corporate world (WW2, Bell labs, IBM and such)
- OSS (GPL, linux, etc)
- MIT/BSD - the era of NPM, composer and such

And continues: "The industry \[snip] now is more and more tending to hypercapitalist approaches that mostly live on everyone's good will's shoulders, while the concentration of wealth and political power further percolates into corporations."

From there, he pointed out that very few OSS projects become "unicorns" anymore.
The ones that do are not winning based on technical merits generally, though; they are winning due to superior marketing.

As such, Marco notes that he feels that market share is not relevant.
We should build software because we want to.
He plans to build and release software as aGPL + commercial; aGPL for OSS consumers, Commercial if you are building your business on it.
This may or may not be a good approach for Laminas.
What we did note, however, is that the current approach means that companies that build on us are not obligated in any way to support the project, and this sort of extractive capitalism is what leads to maintainer burnout and folks leaving the project.

Joey Smith and others note that when they build solutions for others, license _does_ matter, and anything outside MIT/BSD will not work for their clients/businesses.
A license change could jeopardize these sorts of relationships around the project, and steer folks away... and likely also lead to a hard fork.

(We spoke on this subject for a good 30-40 minutes, sharing a number of anecdotes and war stories.)

Basically, this topic gave us a lot of food for thought, but no decisions.
