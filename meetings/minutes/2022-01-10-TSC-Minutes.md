# Minutes from the 2022-01-10 Laminas Technical Steering Committee Meeting

- When: 2022-01-10 at 19:00 UTC, until 19:39 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Aleksei Khudiakov
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Weier O'Phinney

Quorum was NOT met (5 out of 15 members were present).

## Agenda

We did not have an agenda today, but Marco wanted to continue the previous month's discussion around dependency upgrades:

- Lots of them are happening (due to end-of-year PHP minor/major release cycle)
- Would love to automate compatibility with new major releases
- But Dependabot is too noisy

Aleksei pointed out that we had been discussing Renovate bot the previous month, which seemed to answer both the "too noisy" and "automate PHP updates" questions.
Marco pointed out it's more than that; The PHP-FIG evolutions workflow means that we are also doing a bunch of version widening bumps for packages with PSR interfaces (e.g. `psr/log: ^1 || ^2`).
These in particular are doubly noisy, as many of the packages are still with a minimum supported version of PHP 7.3, so they are incompatible with the new FIG major versions.

Luís brought discussion back to Renovate, as he's started using it where he works, and noted that it updates multiple packages in a single PR, bringing down noise.
Gary Lockett (community member) said it can also be configured to open a PR only if tests do not pass.

With some back and forth, we determined that Renovate has Docker containers for running locally, can be run as a GitHub Action, or can be used as a GitHub App.
The latter became the interesting option for those present, as it would require less intervention to roll out to our repositories.

Gary Lockett volunteered to work with Marco to come up with a configuration for us and test it on a number of repositories before we roll out everywhere.
Marco said to start with:

- Lockfile updated daily on current release branch, and merged when green, without a pull request.
- Create a PR for lockfile update issues.
- Create a pull request for new major version support of packages and/or PHP.
