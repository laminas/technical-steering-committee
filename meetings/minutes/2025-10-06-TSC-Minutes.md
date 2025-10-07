# Minutes from the 2025-10-06 Laminas Technical Steering Committee Meeting

- When: 2025-10-06 at 19:00 UTC, until 20:13 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Aleksei Khudiakov
    - George Steel
    - James Titcumb
    - Julian Somesan
    - Marco Pivetta
    - Michał Bundyra

Quorum WAS NOT met (6 out of 16 members were present).

## Agenda

### Release v3 of `mezzio/mezzio-template`

Merge one PR and make a new release for [mezzio/mezzio-template](https://github.com/mezzio/mezzio-template).

#### Discussion

Michał was concerned about the documentation which needs to be updated and about a migration guide to aid users of the package.

#### Decisions

Julian created a poll to vote on this matter and it passed.
The documentation will be updated at a later date, after adding support for Service Manager v4 in other packages.

### Release v3 of `mezzio/mezzio-laminasviewrenderer`

Vote on the release now, to be able to release [mezzio/mezzio-laminasviewrenderer](https://github.com/mezzio/mezzio-laminasviewrenderer) ASAP once the upstream dependencies are released.

#### Discussion

The release v3 of `mezzio-laminasviewrenderer` depends on `laminas-view` Version 3 and `mezzio-template` Version 3.
George mentioned that the package is likely not going to be used before support for Service Manager v4 is added.

#### Decisions

Just like for `mezzio/mezzio-template`, Julian created a poll and it passed.

### Adding 8.5 Support Everywhere

Start testing packages on PHP 8.5 and add support for PHP 8.5.
Since PHP 8.1 is EOL at the end of 2025, drop support for it.

#### Discussion

James agrees with the idea to drop support for PHP 8.1.
Aleksei added that support needs to be added for Service Manager v3 and the code needs to be modernized, especially between PHP 8.1 and 8.2.
George agreed that dropping support for PHP 8.1 would create less work for the code modernization.
The only concern was that PHP 8.1 has EOL 2 months after PHP 8.5 is released.
Aleksei concluded that there is no real need to drop support for PHP 8.1 at this time.

#### Decisions

The TSC members decided in an asyncronous poll that once PHP 8.5 support will be released in a package, the support for 8.1 will be removed in the same PR.
In order to have only 4 PHP versions in composer.json, and reduce the release burden.

### Attending the Dutch PHP Conference

Sponsoring a small booth space at [Dutch PHP conference](https://phpconference.nl/) to raise awareness for Mezzio and middleware architecture.

#### Discussion

Other events were also considered: phpday in Verona, SymfonyCon in Amsterdam.
Aleksei believes that attending will have little benefit.
Aleksei believes the price is too steep and not worth attending without a speaker at the event.
James pointed that the price is too high for the potential awareness, since DPC is not anymore a full PHP conference.

#### Decisions

No decision was made.
The subject of sponsoring conferences will be continued on other TSC meetings.

### Adopt PER Coding Style

The PER Coding Style, currently at the version 3.0, is an evolving standard that keeps up with the PHP releases.
It aims to remain compatible with PSR-12 when practical.

#### Discussion

George and Aleksei agree with the switch.
Still, Aleksei is worried about the amount of work the switch will generate.

#### Decisions

A poll was created to settle the matter and it passed.
SO the `laminas/laminas-coding-standard` will be adapted to PER.
