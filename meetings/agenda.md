# Next Technical Steering Committee Meeting Agenda

- Date: 2024-11-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Archive/Abandon [Laminas Oauth](https://github.com/laminas/laminas-oauth) by [@gsteel](https://github.com/gsteel)

I don't believe we have the resources to maintain this lib.
It is tightly coupled to dependencies that are all aging and mostly archived or in `security-only` mode such as `http`, `math`, `crypt`, `loader`, `config`, `uri`.

### Financing of the Book "Mezzio Essentials"

I would like to discuss the financing of the book "Mezzio Essentials" by Matthew Setter.
I think it would be a good idea to support this project and I see two options:

1. We finance a new version, and with every sale the project receive a share of the revenue.
2. We finance the entire book and is free for everyone.

The biggest question is if Matthew Setter is willing to write a new version of the book and has the time to do so.

See: https://mezzioessentials.com

### Archive & Abandon Various Legacy Libraries

Proposal to archive and abandon a number of un-maintained libs in `security-only` mode:

- [laminas-barcode](https://github.com/laminas/laminas-barcode)
- [laminas-config](https://github.com/laminas/laminas-config)
- [laminas-laminas/laminas-config-aggregator-modulemanager](https://github.com/laminas/laminas-laminas/laminas-config-aggregator-modulemanager)
- [laminas-dom](https://github.com/laminas/laminas-dom)
- [laminas-file](https://github.com/laminas/laminas-file)
- [laminas-http](https://github.com/laminas/laminas-http)
- [laminas-json](https://github.com/laminas/laminas-json)
- [laminas-loader](https://github.com/laminas/laminas-loader)
- [laminas-log](https://github.com/laminas/laminas-log)
- [laminas-math](https://github.com/laminas/laminas-math)
- [laminas-memory](https://github.com/laminas/laminas-memory)
- [laminas-paginator-adapter-laminasdb](https://github.com/laminas/laminas-paginator-adapter-laminasdb)
- [laminas-progressbar](https://github.com/laminas/laminas-progressbar)
- [laminas-tag](https://github.com/laminas/laminas-tag)
- [laminas-text](https://github.com/laminas/laminas-text)
- [laminas-uri](https://github.com/laminas/laminas-uri)
- [laminas-xml](https://github.com/laminas/laminas-xml)
- [laminas-xml2json](https://github.com/laminas/laminas-xml2json)
- [laminas-zendframework-bridge](https://github.com/laminas/laminas-zendframework-bridge)

Additionally, to audit all libs that are marked as discontinued and ensure they are abandoned in packagist and archived on GitHub.

### New major version of laminas-di (by @tuxrampage)

The `laminas-di` component should receive a new major version to improve its
future maintainability and to support new PHP features.

The details for this process are outlined (and discussed) in the following RFC: https://github.com/laminas/laminas-di/issues/95
