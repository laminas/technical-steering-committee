# Minutes from the 2025-01-06 Laminas Technical Steering Committee Meeting

- When: 2025-01-06 at 19:00 UTC, until 20:01 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - Frank Brückner
    - George Steel
    - Julian Somesan
    - Luís Cobucci
    - Marco Pivetta
    - Matthew Setter
    - Matthew Weier O'Phinney
    - Michał Bundyra
    - Rob Allen

Quorum WAS met (11 out of 16 members were present).

## Agenda

No agenda, so free discussion.

- Matthew WOP reminded folks we still have a few open votes on abandoning packages.
- Matthew WOP asked Julian if he needs help with content so we can be listed in the PHPStorm monthly newsletter.
  He confessed that we've not had anything to submit for a couple of months, and that he's unsure what to write about once he gets his planned article on the Problem Details package completed.
  We brainstormed some ideas.
  - Matthew WOP suggested some beginner-oriented tutorials on Mezzio.
    Gary wondered how we would position ourselves against Laravel in that regard.
    Matthew and Rob pointed out that Mezzio allows using a smaller set of dependencies, which is important for companies trying to limit the scope of their SBOM.
    Gary suggested we could also point out where users will hit limitations in Laravel, and how writing against Mezzio could open more possibilities.
  - Marco suggested an architectural "why" post, as this would help him, and other contractors, explain their choices.
    As an example, why use PSR-15-based dispatch versus using an MVC with a mutable request/response.
  - Rob suggested articles about DIC would be useful, particularly positioning our solution against auto-wiring solutions.
  - Gary suggested pointing out benchmarks between Mezzio and other frameworks.
  - Matthew WOP posted:
    > I find I write most of the handlers and middleware myself, but integrate other tooling - DBAL, valinor, paginator, negotiation, session handling, cookie handling, caching, etc. That's what I meant by being able to integrate general-purpose libraries; I don't need to look for a library providing middleware or a full Mezzio integration, just... a library. I then write the integration.
    and later:
    > I feel like PSR-15 + config providers mean that I'm more thoughtful about the boundaries of my software, and more careful about where I introduce integration points.
    Several folks felt that articles detailing this process would be very useful, as they detail the choices we make along the way, and how easy it is to integrate 3rd-party libraries with a PSR-15 architecture.
  - Tom de Wit noted that we should be careful to know our audience, pointing out that Symfony and Laravel make a lot of things so easy that Laminas and Mezzio are a hard sell.
    He suggested talking to a newcomer to Laminas to get their insights on what is difficult and/or to get an idea of how to do something in Laminas versus another framework in order to illustrate the actual effort, and the maintenance cost of each.
    **Illustrate how Mezzio reduces your technical debt.**

At the end, Matthew WOP proposed we commit to a blog post per month.
He will get the minutes posted (you're reading them!), which contain many of the ideas discussed, and then post reminders in the #contributors channel for folks to suggest ideas and/or volunteer to write something for that month.
As a reminder, ANYBODY can write a post for the blog by submitting a PR against the laminas/getlaminas.org repository.
