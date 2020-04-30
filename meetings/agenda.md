# Next Technical Steering Committee Meeting Agenda

- Date: 2020-05-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

- List organizations offering support?
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

- Should we have a list of "companies using Laminas" for the website?
  On the ZF website, we had a section of the homepage that shared logos of
  companies using the framework. This helped establish the breadth of adoption,
  which helped promote the ecosystem.

  Should we do this for Laminas? Matthew has asked the LF legal representative,
  and he has indicated:

  > [The] requirement [...] is that you have permission for us to list their
  > logo. Generally an email request that we display a logo and storing that email
  > will be enough

  Are we interested in doing this?

- GreetBot
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

  I'm willing to pay for this out of my GitHub sponsors funds; do we want to do
  this?

- Future of laminas-cache

  As already stated on [discourse](https://discourse.laminas.dev/t/rfc-laminas-cache-satellite-packages/1543), we should move adapters and plugins into satellite projects.

  - What are the general thoughts of the TSC members about that plan?
  - How long should we wait for feedback from the community?
    - I've seen the [MVC RFC](https://discourse.laminas.dev/t/rfc-zend-mvc-4-design-changes/447) which is around for almost 2,5 years.  

- mezzio-cors library

  max [@boesing](https://github.com/boesing) created an [expressive module](https://github.com/boesing/zend-expressive-cors) which can be used to provide proper CORS details to browsers.
  
  In 2017, he contributed to the MVC module [zfr/zfr-cors](https://github.com/zf-fr/zfr-cors/pull/43) to provide per-route configuration for CORS. As there is no such library which allows project and per-route configuration for CORS in mezzio applications, we might want to move it to the mezzio organization.

  **Questions in case we move it to the mezzio organization**
  - The library uses `options.defaults` in route configuration. Should we change it to `options` instead to keep request attributes clean?

- Mezzio Project - Update

  Create new project to track progress with mezzio components.
  Set the fixed date: 1st of Dec, 2020 (PHP 7.2 has security only support until 30th of Nov, 2020).

  Update all mezzio components:
  - drop support for PHP prior to 7.3
  - add PHP 7.4 build with lowest and latest dependencies
  - add phpstan or psalm
  - update all dependencies to latest version and drop previous versions
  - solve PHPUnit warnings in tests (support only PHPUnit ^9.1)
  - update to LCS v2 (need to be released before)
  - review all open issues and PRs, reply, close or address with new minor/bugfix
  - report tickets for new major (if there is deprecated functionality which should be removed etc)
  - rewrite existing commands to use laminas-cli (keep current commands and mark them deprecated)
  - write new commands or at least reports tickets what commands we should add in each component and link to laminas-cli project

  Order of update does matter, so we can pin latest versions in skeleton/mezzio.

  - Do we want to do this?
  - Can we achieve it?
  - Any other suggestions?
