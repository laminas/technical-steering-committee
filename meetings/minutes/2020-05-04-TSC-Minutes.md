# Minutes from the 2020-05-04 Laminas Technical Steering Committee Meeting

- When: 2020-05-04 at 19:00 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Maximilian Bösing
  - Michał Bundyra

Quorum was met (10 out of 14 members were present).

## Agenda

- Will we list organizations that act as end-user support providers?

  Matthew has had a few companies and contractors ask about having their
  information listed on the site as providing commercial support, and a few
  others asking about what commercial support offerings exist.

  He asked the LF legal representative about if this is allowed, and, if so,
  what stipulations there might be around it. His response:

  > [Y]ou can either have a formal program with criteria or an informal program.
  > If it's a formal program, you list people that qualify. If it's informal, you
  > list people that ask.  If you find that people are just asking to get the logo
  > listed without really supporting, I would recommend a charter for a support
  > program that would list minimum criteria.

  The argument for listing support providers is that it helps establish that
  there's a healthy ecosystem.

  Do we want to list support providers? If so, do we want to do so informally
  (list anyone who asks) or formally (establish criteria)?

- Will we list "companies using Laminas" on the website?
  On the ZF website, we had a section of the homepage that shared logos of
  companies using the framework. This helped establish the breadth of adoption,
  which helped promote the ecosystem.

  Should we do this for Laminas? Matthew has asked the LF legal representative,
  and he has indicated:

  > [The] requirement [...] is that you have permission for us to list their
  > logo. Generally an email request that we display a logo and storing that email
  > will be enough

  Are we interested in doing this?

- Will we use GreetBot in the Slack?
  Last month, when discussing how to reduce noise in Slack, we discussed ways we
  can direct Slack users towards appropriate engagement — e.g., pushing them to
  use the forums to ask questions, reminding them of the TSC meetings, etc.
  Aleksei (@Xerkus) pointed me towards [GreetBot](https://greet.bot) as a
  possible solution.

  Their free plan only provides one message on signup, and a message for joining
  a channel (exactly ONE channel). Their "Plus" plan is $12/month, and offers up
  to 15 messages per user (e.g., a signup message, a reminder a week in, etc.),
  as well as messages per-channel (e.g., to tell them what the purpose of a
  channel is, where to go on the forums for more help, where the docs are,
  etc.). I reached out to see if they have OSS discounts, and they do: half-off.

  Matthew indicates he is willing to pay for this out of his GitHub sponsors
  funds; do we want to do this?

- laminas-cache RFC for splitting adapters out
  As already stated on [discourse](https://discourse.laminas.dev/t/rfc-laminas-cache-satellite-packages/1543),
  we should move adapters and plugins into satellite projects.

  - What are the general thoughts of the TSC members about that plan?
  - How long should we wait for feedback from the community?
    - Max notes the [MVC RFC](https://discourse.laminas.dev/t/rfc-zend-mvc-4-design-changes/447)
      which has been around for almost 2,5 years.  

- mezzio-cors library
  Max [@boesing](https://github.com/boesing) created an
  [expressive module](https://github.com/boesing/zend-expressive-cors) which can
  be used to provide proper CORS details to browsers.
  
  In 2017, he contributed to the MVC module
  [zfr/zfr-cors](https://github.com/zf-fr/zfr-cors/pull/43) to provide per-route
  configuration for CORS. As there is no such library which allows project and
  per-route configuration for CORS in mezzio applications, we might want to move
  it to the mezzio organization.

  **Questions in case we move it to the mezzio organization**
  - The library uses `options.defaults` in route configuration. Should we change
    it to `options` instead to keep request attributes clean?

- RFC for updating Mezzio components
  Create new project to track progress with mezzio components.
  Set the fixed date: 1st of Dec, 2020 (PHP 7.2 has security only support until
  30th of Nov, 2020).

  Update all mezzio components:
  - drop support for PHP prior to 7.3
  - add PHP 7.4 build with lowest and latest dependencies
  - add phpstan or psalm
  - update all dependencies to latest version and drop previous versions
  - solve PHPUnit warnings in tests (support only PHPUnit ^9.1)
  - update to LCS v2 (need to be released before)
  - review all open issues and PRs, reply, close or address with new minor/bugfix
  - report tickets for new major (if there is deprecated functionality which
    should be removed etc)
  - rewrite existing commands to use laminas-cli (keep current commands and mark
    them deprecated)
  - write new commands or at least reports tickets what commands we should add
    in each component and link to laminas-cli project

  Order of update does matter, so we can pin latest versions in skeleton/mezzio.

  - Do we want to do this?
  - Can we achieve it?
  - Any other suggestions?

## Support providers

After Matthew clarified that the purpose is to list organizations that provide
end-user support for Laminas-based applications, and not to list organizations
providing support TO the Laminas Project, the question was "why"? Matthew
pointed out that one criteria decision makers choosing OSS solutions have is
whether or not they can get commercial support. Having some proof that an
ecosystem exists around a project can help in these decisions.

Some concerns were raised that this could be abused to get free advertising for
a company. As such, Matthew reminded attendees that we can either allow
_everybody who asks_ (an _informal_ program), or _anybody who meets criteria we
set_ (a _formal_ program). At this point, several noted that a formal program
seems safest, but that they were unsure if we have the bandwidth to verify.

Marco then proposed that we ask them to provide a non-trivial monetary
contribution, as this would (a) weed out those looking for free advertising, and
(b) help the project reach its funding goals. Matthew noted that the corporate
membership model was going to include membership as a requirement for being
listed as a support provider, so this seemed like a reasonable hurdle. Marco
suggested a $500/year minimum.

Aleksei linked us to the [Drupal commercial vendor program
documentation](https://www.drupal.org/drupal-security-team/information-for-organizations-interested-in-providing-commercial-drupal-7)
as an example of a formal program; it notes that such participants **must** be
involved with a certain number of contributions yearly to be listed, as well as
pay a yearly fee ($3k - similar to the original general corporate memberships we
were attempting last year). Marco indicated maybe he was starting to low with
his suggestion.

Luís asked what would happen if we received complaints about a provider. Matthew
noted that sponsorship is a _gateway_ to being listed as a support provider, but
not a _guarantee_.

### Summary

While we had consensus that we likely want to do this, we still had a lot of
questions about the actual mechanics, and decided to table the topic for further
discussion.

## Listing "who uses Laminas" companies

Frank opened by asking if we had anybody interested in the first place; the
answer is "yes". Matthew notes that the primary motivation is to demonstrate a
robust ecosystem of users, across a broad range of companies; again, the goal is
to provide decision makers with confidence that they can adopt Laminas for their
projects.

Generally speaking, everyone felt we wanted to do this, but also that we should
likely be picky.

Aleksei suggested asking not just for the company name and logo, but for a case
study of how they _use_ Laminas. This provides even more information for
decision makers, and gives us more criteria for selecting to display them. He
also suggested we could have a "case studies" section of the website, but
cherry-pick from submissions for display on the home page.

Marco suggested a TSC vote for any that we include on the home page.

### Summary

We voted to:

- Create a special issue-type for the getlaminas.org website repository for
  submitting a case study, which will include a checkbox indicating a request to
  list on the website.

- Case study submissions will be published on a special section of the website.

- Case studies opting-in to the home page will then be voted on by the TSC
  before listing on the home page.

## Intermission

At this point Luís and Andreas had to leave. We still had 8 out of 14, meaning
we had quorum, so we decided to continue.

## GreetBot

Matthew noted that in our brainstorm last month, we agreed we want to direct
users to the forums as much as possible, but also remind them periodically (as
channel topics are easily overlooked). Aleksei suggested
[GreetBot](https://greet.bot).

Matthew looked into it, and the free tier does not provide the features we want,
and the paid tier was $12/month. He emailed the company and asked about OSS
discounts, and they said $6/month for OSS organizations. He is willing to pay
that from his GitHub sponsorship funds.

Geert asked what the features we need are. Matthew noted:

- Messaging on joining the Slack.
- Messaging on joining specific channels.
- Periodic messaging to remind users of forums and guidelines.

As Aleksei notes, while the first can be easily handled by our bot, the next two
are worth paying for.

### Summary

We voted to enable the GreetBot, with the understanding that if we need an app
integration slot later, or we find it's not achieving the goals we want it for,
we will remove it.

## laminas-cache

Max posted an RFC for splitting the various laminas-cache adapters into
satellite packages:

- https://discourse.laminas.dev/t/rfc-laminas-cache-satellite-packages/1543

He wants to know primarily:

- Is the approach valid?
- How long should we wait for community feedback?

Marco wondered if a BC-compliant split would be possible, but we quickly
realized that if the goal of the satellite packages is partially to allow
providing platform requirements in the packages, this would break BC immediately
for just about everyone. Eventually, Max clarified that the approach would be as
follows:

- Initial satellite package versions WOULD NOT introduce platform requirements,
  and would use the existing namespaces from laminas-cache (to prevent users
  from needing to make any code changes).
- Initial version of each satellite package would require a new minor version of
  the laminas-cache version itself in order to obtain dependencies.
- The new minor version of the laminas-cache package would remove code now in
  the satellites, and require each of the satellite packages. This allows it to
  retain backwards compatibility.
- A new major version of laminas-cache would require a
  laminas/laminas-cache-storage-implementation virtual package, and remove
  dependencies on any of the satellite packages providing storage capabilities.
- A new major version of each satellite would introduce platform requirements.

Aleksei argued that the satellite packages should have their own namespaces, as
that would allow installing them individually in parallel with the original
laminas-cache package, and the laminas-cache package could then mark the
adapters as deprecated. Max argued this puts too much onus on users to make
changes to their code; that it's simpler to know that when you update to the new
major version, you also must install an adapter package. Additionally, it
prevents the need for marking packages as replacements or as being in conflict
with any particular laminas-cache versions.

### Summary

We voted to approve the RFC for immediate development.

## Wrapping up

At this point, Geert also had to leave, which meant we no longer had quorum. We
decided to move undiscussed items into the TSC channel, voting if we reach any
conclusions, and otherwise pushing them to next month's meeting.

The meeting lasted 118 minutes. All votes taken were unanimously decided, though
we pushed some discussions to future dates.

The next meeting will occur at 19:00 UTC on June 1, 2020.
