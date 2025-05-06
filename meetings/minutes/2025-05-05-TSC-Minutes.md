# Minutes from the 2025-05-05 Laminas Technical Steering Committee Meeting

- When: 2025-05-05 at 19:00 UTC, until 20:44 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Aleksei Khudiakov
    - Frank Brückner
    - George Steel
    - Julian Somesan
    - Luís Cobucci
    - Matthew Setter
    - Rob Allen

Quorum was met (8 out of 16 members were present).

## Agenda

### Release version 3.0 of laminas-filter

The tasks from the [milestone](https://github.com/laminas/laminas-filter/milestone/4) and the [Migration from Version 2 to 3](https://github.com/laminas/laminas-filter/blob/3.0.x/docs/book/v3/migration/v2-to-v3.md) are complete.

The attendees swiftly agreed to create a poll for releasing decoupled libraries.
The poll passed on the following day.

### Release version 1.0 of laminas-navigation-view

Again, there was little to discuss, but there was mention of splitting large Laminas packages into smaller, more easily managed dependencies.
George Steel worked on refactoring [laminas-navigation-view](https://github.com/laminas/laminas-navigation-view) and getting it ready for the 1.0 release.
Aleksei mentioned agreed that the decoupling process is desirable.

The poll from the previous item in the agenda also covers this topic.

### General Discussion on Soft-Dependency Satellite Packages

Decoupling was discussed at length as a solution for dependencies that prevent some Laminas packages from being updated.
The dependency between [laminas/laminas-paginator](https://github.com/laminas/laminas-paginator) and [laminas/laminas-servicemanager](https://github.com/laminas/laminas-servicemanager) was discussed in detail.
The members agreed that releasing a decoupled version of any package would be backward incompatible, so it would warrant a major version release.
At the same time, each decoupling must be investigated on a case by case basis, to analyze all trade-offs.

The agreement was to manage the split when the next major version is worked on for each package.

### The Future of MVC

The discussion regarding [Laminas MVC](https://github.com/laminas/laminas-mvc) was the most sensitive and engaging.
Laminas MVC has received little attention due to most of the focus going to laminas-servicemanager and the middleware architecture.

Julian, Aleksei, George, Rob agreed that any more work on keeping MVC up to date would require too much work and expertise from TSC members who are too busy for it.
Equally, documenting a migration from MVC to Mezzio was not attractive to anyone.
Still, an abstract migration guide could be built while working on actual projects migrating to Mezzio.

#### Conclusions

The shift of focus toward middleware, PSR-7, PSR-15, PSR-17 must be publicized as a collective effort.
Laminas MVC must not be archived yet, but put in `security only` mode until PHP v8.5, to allow developers of legacy applications to adapt to its eventual abandonment.

A poll was created and soon after passed.
The members agreed to add deprecation notices immediately to direct users to the Mezzio alternative instead.

### BSD-3 license clarifications

Julian asked for a clarification related primarily to the 3rd clause of the [BSD-3 License](https://opensource.org/license/bsd-3-clause).
The discussion related to it was continued with Matthew Weier and a representative of the Laminas Foundation.
The conclusion was that if the usage complies with the below document, no permission is required:
[Linux Foundation Trademark Policy](https://lfprojects.org/policies/trademark-policy/)
