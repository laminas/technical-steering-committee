# Minutes from the 2022-03-07 Laminas Technical Steering Committee Meeting

- When: 2022-03-07 at 19:00 UTC, until 21:00 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brückner
  - Geert Eltink
  - Marco Pivetta
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra
  - Witold Wasiczko

Quorum WAS met (10 out of 15 members were present).

## Agenda

### Solidarity with Ukraine

In the #contributors channel, there have been some calls for the project to show solidarity with Ukraine, with a number of possible approaches:

- Adding banners to the documentation sites
- Adding verbiage to the README file of each repo
- Adding verbiage into releases via automatic-releases
- Adding a message in the command/version line of laminas-cli

Matthew noted that adding a banner to the documentation sites would require re-compiling docs for all repos.
Frank answered that this can be scripted due to the fact we added a trigger to the docs build workflows.
Michał indicated he could drop in README changes via a script quite quickly.
Max asked if we'd do releases immediately, or just push the README.
Matthew followed up, asking if releases were really necessary, as the file would be on the landing page for the repository.
Several chimed in at this point that existing users will look at new releases, while new users will go to the landing page.
As such, having both would give greatest coverrage.

Marco stated that having banners likely won't have impact, as they are likely not visible in Russia.
However, code files installed as part of dependencies might, so his suggestion is code commit and releases.

Aleksei said he doesn't think any of this will have impact.
His experience as a Russian is that political messages do not get attemtion, due to the consistent propaganda they receive.
His feeling is only when something inconveniences people do they stop and notice — for example, when a service is cut off.

Gary Lockett asked if pointing to protests in St Petersberg and Moscow might have more effect.
Aleksei agreed that it might.
We brought in Anna Filina to the conversation to get some opinions, and to see if she might be able to craeft a message.
We also discussed the fact that if we link to a single, specific document, we can modify that document over time, so that we don't have to craft a message immediately.

After some back and forth, we decided to:

- Anna volunteered to write a message, via a PR on the Laminas .github repo, so that we can review; when ready, she will translate.
- We will then push this message into the `README.md` file of all repositories.
  Michał volunteered to write a script to do this.
- Matthew W O'P volunteered to write a blog post for the getlaminas.org website, and will create a PR against its repo for review.

### Code coverage

George Steel proposed we adopt code coverage of some sort, as a metric to help improve PR quality and ensure new features have reasonable tests.
As this has come up before, Matthew W relayed a message from Luís Cobucci (absent for the meeting) that he felt that mutation testing is a far better metric.
Marco agreed, and indicated he's working on some proposals around this for PHPUnit, but that it really must be restricted to diffs only, to ensure the score is only for feature changes or additions.
As he noted, mutation testing encourages reducing code complexity, and this in turn helps improve quality.

George pointed out that he was raising the issue based on another maintainer wanting coverage metrics last year to assist with review.
Aleksei pointed out that coverage tools do not provide great tooling in GitHub for detailing _why_ tests are insufficient.
Marco and Matthew pointed out that mutation testing will help reviewers understand impact on the component, and help them guide contributors to make the contribution better.
Additionally, the tooling has great support within GitHub, hihlighting each problematic line and providing explanations.

In sum, we decided not to use coverage, and Marco will outline what needs to be done for us to add mutation testing.

### Phone validation

George Steele indicates that we have a large number of issues in laminas-i18n around phone number validation.
He suggests leveraging giggsey/libphonenumber-for-php to be the backing data/library for these validations and filters, as this is kept up-to-date, and our users would not need to wait for updates from us to get updated formats.

There was general agreement that this was a good plan; the main point of contention was how to go about it.

### api-tools-oauth2

Witold noted that we are unable to update laminas-api-tools/api-tools-oauth2 to PHP 8.1 due to the fact that bshaffer/oauth2-server-php appears to be unmaintained.
He suggested one of the following:

- Fork unmaintained repository and develop under Laminas.
- Change server implementation (e.g. `league/oauth2-server`).
- Create abstraction for oauth2 server and create satellite repositories with desired implementation.

Marco noted that the author has been responsive to mentions, and will likely be willing to merge something if we provide him a solid patch.
Witold pointed out that the patch is not entirely trivial, as the library needs to be migrated to GitHub Actions first, as its tests can no longer run on Travis-CI.
Matthew gave Witold some pointers to how to make that happen, and offerred to assist in the coming days.

We agreed that getting the existing backing library updated would be the quick win.
We should only plan a migration if the library won't be suitable long-term.
