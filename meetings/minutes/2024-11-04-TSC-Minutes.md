
# Minutes from the 2024-11-04 Laminas Technical Steering Committee Meeting

- When: 2024-11-04 at 19:00 UTC, until 20:06 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - George Steel
  - Julian Somesan
  - Matthew Setter
  - Michał Bundyra

Quorum WAS NOT met (6 out of 16 members were present).

## Agenda

### Archive/Abandon Laminas Oauth

George proposed to archive Laminas Oauth because there are no resources to maintain it.

#### Discussion

Aleksei mentioned that Oauth 2 and OIDC are superior. 

#### Decisions

The other members agreed and an async poll was created. The vote passed on the following day.

### Financing of the Book "Mezzio Essentials"

Frank proposed financing the book "Mezzio Essentials" by Matthew Setter. 

#### Discussion

Frank gave two options: to finance the new version of the book and get a share of the revenue; or to finance the whole book and make it free for everyone. Julian mentioned that the book would also benefit from associated videos. 

#### Decisions

The members agreed that the matter needs to first be discussed with Matthew before it is brought back to the TSC. Also Matthew Weier (mwop) must confirm that the Laminas Foundation funds can be used for the book.

### Archive & Abandon Various Legacy Libraries

The proposal is to archive several libraries that are currently in security-only mode. Also to audit all libs that are marked as discontinued and ensure they are abandoned in packagist and archived on GitHub.

- laminas-barcode
- laminas-config
- laminas-laminas/laminas-config-aggregator-modulemanager
- laminas-dom
- laminas-file
- laminas-http
- laminas-json
- laminas-loader
- laminas-log
- laminas-math
- laminas-memory
- laminas-paginator-adapter-laminasdb
- laminas-progressbar
- laminas-tag
- laminas-text
- laminas-uri
- laminas-xml
- laminas-xml2json
- laminas-zendframework-bridge


#### Discussion

Aleksei weighed in on several packages:

- laminas-barcode - not unless good actively maintained alternative
- laminas-config - abandon because of array access which has many many quirks
- laminas-config-aggreggator - leave active because it has support for modulemanager modules
- laminas-dom - sunset because of php 8.4 dom changes
- laminas-file - abandon; class locator in file system?
- laminas-json - abandon because json is now in php core
- laminas-loader - useless in mainstream codebases with composer
- laminas-log - abandon because PSR was out long enough
- laminas-math - abandon; wrapper over bigint and the other similar extensions
- laminas-memory - abandon; cache with memory adapter highlighted like we have virtually no userland control over memory in php
- laminas-paginator for laminas-db - abandon when laminas-db is abandoned
- laminas-progressbar - abandon because of low usage
- laminas-tag - abandon; tag clouds?
- laminas-text - abandon; figlets? ascii tables?
- laminas-xml - do not abandon; xml is the most stable thing
- laminas-xml2json - abandon because it depends on laminas-json
- laminas-zendframework-bridge - abandon because it's only needed by legacy code

Julian mentioned that Adobe's Magento depends on many Laminas packages. George is in favor of abandoning packages to lower the number of PRs for the next version of PHP, though he suggested that laminas-http, laminas-uri and laminas-xml be left active.

#### Decisions

Julian offered to create a poll in adoodle.org regarding the remaining packages proposed to be archived. He needs to first build a list of emails from the TSC members.
