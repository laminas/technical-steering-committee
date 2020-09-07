# Next Technical Steering Committee Meeting Agenda

- Date: 2020-09-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

 - "Commercial vendor" program proposal. Certain vendors may wish to financially contribute to Laminas Projects. There seems to be a feeling that there should be some "criteria", which Linux Foundation calls a "formal program". [Drupal Commercial Vendor program](https://www.drupal.org/drupal-security-team/information-for-organizations-interested-in-providing-commercial-drupal-7) is similar in nature, but a little more complicated. @asgrim suggestions as a starting point (we can discuss and refine/replace/improve this list):
    - Financial annual contribution, perhaps with tiers for different contribution levels (e.g. $500/year "community" tier, $1,000/year "standard", $3,000/year "premium")
    - At least 2+ contributions per month from the company (e.g. an employee at the company). A contribution can be any number of things (attending a TSC meeting, code contribution, code review/triage issues, documentation, general maintenance, support, etc.)
    - Active "promotion". Loose definition is intentional, but can be a two-way street. Vendor should promote Laminas/Mezzio/API Tools, and Laminas should promote the vendor (according to the level of contribution). "Promotion" is vague on purpose, could be tweets, could be blog posts, logos on pages, recommendations to clients (although, always use the right tool for the job - vendor does not have to exclusively use Laminas/Mezzio/API tools etc!) or Laminas recommending services of commercial vendors etc.
    - Perhaps a minimum committment term (for example 2 or 3 years initial committment, then renew year-on-year as agreed)
    - Agreement that the vendor adheres to the Code of Conduct (critically: vendor should not bring Laminas Projects into disrepute)
    - TSC could have power to vote on whether a partnership with a "commercial vendor" is in the best interests (e.g. perhaps the TSC feels a vendor is not contributing, or has brought the project into disrepute with their actions etc.)

- Hacktoberfest
  
  - [Hacktoberfest](https://hacktoberfest.digitalocean.com/) is incoming and we can take advantage of that event. As we are still searching for maintainers and want to encourage developers to contribute to laminas, we could start focusing on repositories which have open TODOs. These TODOs might be one of the following:
  
      - PHP 8 support + CI setup (should we create a HOWTO for this?)
      - Adding psalm + CI setup (should we create a psalm configuration template?) 
      - Adding `laminas/automatic-release` to packages which should be migrated to the new release process (should we create a HOWTO for this?)
      - *More ideas welcome!*
  
    We definitely should create a "hacktoberfest" label for all our packages. If there are already issues which could be fit the hacktoberfest event, we can label these right after the label creation.
  
  - Can we mark `Good First Issue` as `hacktoberfest` directly?

