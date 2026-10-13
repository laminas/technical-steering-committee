# Minutes from the 2026-10-05 Laminas Technical Steering Committee Meeting

- When: 2026-10-05 at 19:00 UTC, until 20:50 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Rob Allen
    - Frank Brückner
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - Marco Pivetta
    - Julian Somesan
    - George Steel
    - Matthew Weier O'Phinney

Quorum WAS met (8 out of 16 members were present).

## Agenda

### PHP 8.6

PHP 8.6 is the next major release of PHP, scheduled for 19 November 2026.
The members considered the options of forming a team to carry out the update process versus automating it with Rector.

#### Discussion

Marco mentioned that most of the work is fixing tiny things.
Matthew added that the biggest issue is updating the versions for PHPUnit, Psalm, and phpcs.
George reminded the team that PHP 8.2 is EOL, so it has to be removed from `.laminas-ci.json`.

Most of the discussion focused on updating support for PHPUnit, considering the issues when the update to PHP 8.5 was implemented.
George said that the process could be automated into [laminas/internal-tooling](https://github.com/laminas/internal-tooling/).

Aleksei considered that keeping Psalm and structarmed is not worth it because of the extra work they require during PHP version upgrades.
Marco and George argued that these tools are vital in revealing cracks/shifts in dependencies.
They also added that Mago is beneficial because it has no dependencies - the opinion was upvoted by Frank and Rob.
Still, George advised against switching to Mago at the same time as upgrading the PHP version.

#### Decisions

George offered to update `laminas/internal-tooling` and evaluate the results for a couple of repos.
The alternative is to provide canonical PRs as examples for contributors.

### Note PHPStorm Providing Licences Somewhere on the Website

Publicly acknowledge the receipt of JetBrains licences for their all-products pack on the https://getlaminas.org/ website.

#### Decisions

It was agreed to add a JetBrains mention to the site.
Either George or Julian will create a PR.

### Change Renovate config to bump dev deps instead of updating the lock

Renovate `rangeStrategy` with `"matchDepTypes": ["require-dev"], "rangeStrategy": "bump"`.

#### Discussion

Mario began by saying he is against `widen` because it impacts the guarantees given by CI and static analysis, and `composer update` can pull in very outdated deps downstream.
He added that dev deps should be bumped because end users never see them, and tests should run only for the latest versions.
George leaned toward bumping everything per minor release.

Aleksei believed that bumping dev deps could narrow the effective `require` range for transitive dependencies, making lowest-deps CI targets misleading or useless, when they can in fact highlight problems.
He recommended version bumps for tooling, but only selectively for other libraries (e.g., when resolving Psalm).

#### Decisions

The members agreed that dev-dep bumps currently happen manually and dependency changes generally warrant a minor release.
A poll was passed in favor of changing the Renovate policy for require-dev to `bump`.

### Article on the Impact of AI Coding Assistants on Frameworks

The article explores the advantages of a minimal, standards-based core like Mezzio, compared to full-stack frameworks.

#### Discussion

Marco did not want to contribute to the conversation, given that he is against using AI in coding in general.

Matthew opined that he is ok with AI, which handles the Mezzio-based apps fine.
He believed this is thanks to the platform using solid coding principles (DI, single responsibility, tight CS standards, extensive test examples).
He also added that coders don't need AI in the Mezzio core.

Julian argued that AI is not going away, citing a recent JetBrains survey where 80% of responders use AI.
Matthew considered the survey biased because those users are already using AI via PHPStorm.

George opined that Mezzio would be better suited for AI avoidants.
He added that a better angle for the article is 'configuration vs convention' as a way to test if AI is using the code correctly.
Frank and Matthew Setter agreed with this assessment.
George was against competing with other frameworks that have already won the popularity contest against Mezzio.

#### Decisions

Julian will discuss the points raised here with the article's author.
