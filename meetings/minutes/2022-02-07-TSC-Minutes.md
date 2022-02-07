# Minutes from the 2022-01-10 Laminas Technical Steering Committee Meeting

- When: 2022-02-07 at 19:00 UTC, until 19:57 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Bruchner
  - Geert Eltink
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra
  - Rob Allen

Quorum WAS met (9 out of 15 members were present).

## Agenda

### Updates on Renovate Bot

Last month, a small working group (Gary Lockett, Marco Pivetta) started collaborating on configuration and workflows for Renovate Bot.
Matthew asked for a status.
Marco reported that it does the following:

- Automatically update `composer.lock` each night, without a pull request.
- On test failures following ^^, open a PR.
- Automatically widen ranges for new major releases in `composer.json` and create a PR.
- Separate patches for `laminas/*` upgrades, as well as other repositories.

Matthew asked what the next steps would be.
Gary answered that:

- CI actions would need to be enabled on push eventse for branches with the prefix `renovate/*`.
- The lockfile must be generated using a Composer 2.2+ version.
- The `config.platform.php` version must be set in `composer.json`.

Matthew asked if this means touching each and every repo, and, if so, we might want to do it in conjunction with setting up org-level workflow templates.
Additionally, he asked if this would require new releases, or could be done on the default branch without triggering a release.
Marco indicated in the affirmative for each of these points.

Max asked about the `config.platform.php` setting, pointing out that this might cause issues with our CI jobs, as the dependencies installed would only be for that platform.
After some back and forth, Matthew suggested that in the CI container, we **always** remove that setting before running a job.
Marco said this would work fine, and we agreed to this.

Matthew summarized what needs to happen:

1. We need to update the CI container to strip `config.platform.php` settings before executing jobs.
2. We need to add an org-level workflow CI definition that we can then reference in repo-level workflows.
3. We need to update individual repos to (a) add the config.platform.php value, (b) update the lockfile, and (c) update the CI workflow.
4. We enable Renovate on all repos we touch for (3).

Matthew volunteered to do 1 and 2.
3a can likely be accomplished with `jq | grep | composer config`, which then allows (b) to be run immediately.
If a workflow does not differ from standard, we can likely `wget` a standard one to drop in.
Matthew volunteered to write up steps to update repos; Gary Lockett pointed him to [docs he's already written as well](https://github.com/laminas/.github/blob/main/RENOVATE.md).

Max indicated he's not happy with having a `config.platform.php` setting that is specific to a GitHub App.
Marco pointed out it's not just for that, but to prevent creation of lockfiles that target something other than the minimum supported PHP version.

### Is laminas-db abandoned?

Per a contributor and user:

- We have 15 opened pull request and 11 opened issues.
- We have 3 non active mainteners on "laminas-db" project.
- Last merge was 4 months ago.
- Version 3 is not developed since 31 Dec 2019.
- Unit tests have errors.
  Volunteer developers cannot complete the quest with CI on github and stop making contributions.
  For example, in laminas/laminas-db#232, the comment was changed, but the test failed!
  Give us local instrument for run tests (the best is Docker images on official repository).
- Tests for Oracle are not support on CI.

Marco felt that the original reason to re-open laminas-db was likely driven by Zend to allay customer concerns, likely around IBM DB2.
Matthew said he couldn't comment, other than to say it wasn't really about DB2.
He indicated he'd spoken to the maintainers, and they were in a situation where they each _want_ to help maintain the library, but that their jobs keep them too busy to do so.

Matthew's primary concern is what happens to existing users (there are a LOT of package downloads, and it's a key part of Laminas API Tools).
For him, having a migration path from laminas-db to Doctrine DBAL would be ideal, whether that's a wrapper (easiest for adapters and basic queries, difficult for SQL abstraction), or some sort of migration tooling (which hits on the SQL abstraction difficulty).

We opened votes then to:

- Remove the current laminas-db maintainers
- Mark the laminas-db package as feature-complete, with the exception of adding support for new PHP versions

Both votes passed.
We decided that any migration tooling or wrappers would require an RFC before making further decisions at this point.
