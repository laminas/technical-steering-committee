# Minutes from the 2022-04-04 Laminas Technical Steering Committee Meeting

- When: 2022-04-04 at 19:00 UTC, until 19:52 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Andreas Heigl (arrived late)
  - Frank Brückner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Max Bösing

Quorum WAS met (7 out of 14 members were present).

## Agenda

### RFC to simplify laminas-view

[George Steel](https://github.com/gsteel) (community member) has proposed an [RFC to simplify laminas-view](https://github.com/laminas/laminas-view/issues/149).
The immediate response from members of the TSC was (a) the simplifications look good, but (b) we have concerns about BC impact and migrations.
The main migration concerns are around MVC-specific features: rendering strategies, view events, and URLs.
Matthew suggested we create a laminas-mvc-view package for those integrations, which would largely resolve BC issues.
That said, there will be places such as mezzio-laminasviewrenderer and components that provide view helpers and strategies that will need clear migration paths and tooling.

Marco suggested a development spike to validate, and Matthew asked George if he's done any development yet.
He indicated he has not, as he's been waiting for feedback on how much he can break.
We suggested he go ahead and start, and gave him some feedback and ideas on how to do so iteratively.

### Composer v1 support

Max has proposed we potentially drop support for Composer v1 in our Composer plugins, as we've had test failures under PHP 8.1 when testing against Composer v1.
Discussion pointed out that our own packages support 7.3 or 7.4 and up, meaning we have no meaningful reason to support earlier Composer versions.
Dropping the v1 requirement in a new minor release and removing the v1-specific code would still be backwards compatible, as this is utility code not meant for extension.

We agreed to drop v1 support.

### laminas-servicemanager and container-interop

Max has proposed a number of ideas for removing our dependency on container-interop, and allowing us to move to official PSR-11 support, within laminas-servicemanager.
We originally had a rather [large RFC to discuss](https://github.com/laminas/technical-steering-committee/blob/6c7973d082cbafad4c1b5710ab4e69f15464a231/meetings/agenda.md#laminas-servicemanager-container-interop-further-actions), but late last week, Matthew suggested to the TSC that we go with the originally proposed solution from last year: mark laminas-servicemanager as a replacement for container-interop, and have it internally `class_alias` each container-interop interface to the equivalent PSR-11 interface.
We decided that this would be the most expedient route, and make it possible to switch to PSR-11 interfaces in the next minor after such a release.
The reason it works is because laminas-servicemanager currently only explicitly defines container-interop parameter type hints; since container-interop v1.2 and later extend PSR-11 interfaces, switching them to PSR-11 is considered type widening in this context, which makes them compatible.
Since no return type hints are explicitly defined, and because the two interfaces have the same API, we can change the return types without side effects at this time.
With class aliases, the two become equivalent within Laminas code bases.

We will need to provide tooling in the form of Rector rules or CLI scripts to help people update factories that define typehints on container-interop to update them for the minor release where we drop support for container-interop.

Members agreed that this was ready to go; Matthew will review the [existing pull request from Max](https://github.com/laminas/laminas-servicemanager/pull/96/) and start the process.
