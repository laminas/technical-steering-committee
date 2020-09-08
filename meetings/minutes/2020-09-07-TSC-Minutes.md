# Minutes from the 2020-09-07 Laminas Technical Steering Committee Meeting

- When: 2020-09-07 at 19:00 UTC, until 20:15 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Geert Eltink
  - James Titcumb
  - Luís Cobucci
  - Marco Pivetta
  - Max Bösing
  - Witold Wasiczko
  - Matthew Weier O'Phinney

Quorum was met (9 out of 15 members were present).

## Agenda

- "Commercial vendor" program proposal. ([jump to discussion](#vendor-program))

  Certain vendors may wish to financially contribute to Laminas Projects. There
  seems to be a feeling that there should be some "criteria", which Linux
  Foundation calls a "formal program".  [Drupal Commercial Vendor
  program](https://www.drupal.org/drupal-security-team/information-for-organizations-interested-in-providing-commercial-drupal-7)
  is similar in nature, but a little more complicated. @asgrim suggestions as a
  starting point (we can discuss and refine/replace/improve this list):

  - Financial annual contribution, perhaps with tiers for different contribution
    levels (e.g. $500/year "community" tier, $1,000/year "standard", $3,000/year
    "premium")

  - At least 2+ contributions per month from the company (e.g. an employee at
    the company). A contribution can be any number of things (attending a TSC
    meeting, code contribution, code review/triage issues, documentation, general
    maintenance, support, etc.)

  - Active "promotion". Loose definition is intentional, but can be a two-way
    street. Vendor should promote Laminas/Mezzio/API Tools, and Laminas should
    promote the vendor (according to the level of contribution). "Promotion" is
    vague on purpose, could be tweets, could be blog posts, logos on pages,
    recommendations to clients (although, always use the right tool for the job
    — vendor does not have to exclusively use Laminas/Mezzio/API tools etc!) or
    Laminas recommending services of commercial vendors etc.

  - Perhaps a minimum committment term (for example 2 or 3 years initial
    commitment, then renew year-on-year as agreed)

  - Agreement that the vendor adheres to the Code of Conduct (critically: vendor
    should not bring Laminas Projects into disrepute)

  - TSC could have power to vote on whether a partnership with a "commercial
    vendor" is in the best interests (e.g. perhaps the TSC feels a vendor is not
    contributing, or has brought the project into disrepute with their actions
    etc.)

- Hacktoberfest ([jump to discussion](#hacktoberfest))
  [Hacktoberfest](https://hacktoberfest.digitalocean.com/) is incoming and we
  can take advantage of that event. As we are still searching for maintainers
  and want to encourage developers to contribute to laminas, we could start
  focusing on repositories which have open TODOs. These TODOs might be one of
  the following:
  
  - PHP 8 support + CI setup (should we create a HOWTO for this?)
  - Adding psalm + CI setup (should we create a psalm configuration template?) 
  - Adding `laminas/automatic-release` to packages which should be migrated to
    the new release process (should we create a HOWTO for this?)
  - *More ideas welcome!*
  
  We definitely should create a "hacktoberfest" label for all our packages. If
  there are already issues which could be fit the hacktoberfest event, we can
  label these right after the label creation.
  
  - Can we mark `Good First Issue` as `hacktoberfest` directly?

## Hacktoberfest

In past years, we have only supported Hacktoberfest passively, by coincidentally
merging pull requests that users participating in the event provide to the
project. Max has proposed that we be a bit more active around it this year, and
have some specific projects with labelled issues available for participants to
work on.

Marco suggested we potentially add some verbiage to the issue and PR templates
to let folks know to look for the labelled issues during that month. Matthew
suggested that we maybe do a blog post indicating what projects we are pushing
during the event, how contributors can help out, and then link to that blog post
from the issue templates.

Max proposes several things:

- First, that we try and get the automatic-releases workflow rolled out before
  the event, to make it easier.
- We create a label specific to Hacktoberfest, and roll it out to all repos.
- We ask Hacktoberfest participants specifically to help with the PHP 8 and
  Psalm projects, and create issues on all repos that do not have PHP 8 support
  and/or Psalm CI/CD integration setup, marking them with the new Hacktoberfest
  label.

Max volunteered to create a script that creates these issues, and will ask for
help in getting information out to users as needed. Prior to that, he will write
up instructions for how the tasks should be accomplished, and will link to that
write-up in the issues he generates.

## Vendor Program

We originally discussed the idea of commercial vendors and/or support programs
earlier this year. At the time, the Linux Foundation indicated to us that we
need to either do a "let anyone who asks in" program (an "informal program"), or
have a published set of criteria by which an organization may be listed (a
"formal program"). We voted to do a formal program, but never pushed forward
what that would look like.

James put together some ideas based on the Drupal Commercial Vendor Program, as
noted in the agenda above.

The initial question raised is that the various "tiers" would mean for an
organization. Matthew noted that it could be used to determine how much
visibility they have on the website: a text link, a logo, a blog post, etc.
However, he also indicated he wasn't entirely sold on tiers at this point, and
James noted the same as well. Everyone agreed, however, that a financial
contribution was a reasonable and expected gateway.

At this point, we decided we'd likely stick with a single amount.

Matthew indicated he really liked the second clause, which required ongoing,
non-financial contributions, as this makes the program more collaborative. Marco
pointed out, however, that this sort of commitment could weed out companies that
have no problem contributing money, but might have too much red tape or process
in place to make other contributions possible.

Witold pointed once again that the point of the formal program is to weed out
those for whom this is just "cheap ads". In other words, the program is intended
to ensure that those listed will actually benefit the Laminas community by being
present in the ecosystem.

Aleksei suggested that we use the tiers as commitment levels, with higher
amounts of non-financial commitments required at higher tiers, and that we would
reciprocate by allowing them to introduce vendor-specific tutorials and/or
branding within the documentation. Alternately, we could label contributions
made by partners.

Several folks pointed out that we should hold a vote to approve new vendors;
Matthew pointed out that the last caluse would cover both voting to approve new
vendors, as well as to boot those we feel are a detriment to the project (not
adhering to the CoC, denigrating the project publicly, providing poor service to
customers, etc.). Marco indicated we should have such votes trigger immediately
on a new submission, so it's not a month before they hear back from us.

Marco moved that we make the initial program as simple as possible, with as few
requirements as possible, so that we can see if it will even be of interest. We
can always vote to change it later should we notice issues arise. As such, he
suggested a financial contribution with a minimum commitment only, and after
some discussion, we boiled it down to this:

- Commercial vendor/support providers will provide $1000 yearly for a 3 year
  minimum to the project.

- Commercial vendor/support provider will adhere to the Code of Conduct
  (critically: vendor should not bring Laminas Projects into disrepute).

- TSC could have power to vote on whether a partnership with a commercial
  vendor/support provider is in the best interests (e.g. perhaps the TSC feels a
  vendor is not contributing, or has brought the project into disrepute with their
  actions etc.).

At this point, we held a vote to accept the above, which passed unanimously.

Matthew will contact the Linux Foundation to work out the precise wording and
any legal issues, and then get back to the TSC with any changes and/or the final
document for us to post.

## Automatic Releases workflow

As one final request before ending the meeting, Matthew asked that each TSC
member try and take on at least one repository to convert to the
automatic-releases workflow. James asked if there was a checklist of repos that
needed it, and Matthew answered "any that we didn't vote to mark security-only".
James would like a list so he doesn't have to look up that information, so
Matthew agreed to provide that this week.
