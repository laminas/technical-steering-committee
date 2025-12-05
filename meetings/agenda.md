# Next Technical Steering Committee Meeting Agenda

- Date: 2026-01-12
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Release Laminas Paginator v3

The next major of paginator is ready to go: [V3 Milestone](https://github.com/laminas/laminas-paginator/milestone/3?closed=1)

- Removes caching from the Paginator (Dependent on Laminas Cache)
- Adds a "CachingAdapter" using PSR-6 for decorating any adapter
- Removes Laminas\Db Adapters
- Removed Laminas\View Integration (With the expectation that a small lib will be created to integrate the 2)
- Add SM v4 Support
- Remove static properties used for configuration (Default scrolling style etc)
- Remove "Paginator::toJson()" - no idea why that was there.
- Local dev tooling improvements and CI/QA improvements
- Introduce `PaginatorFactory` for easy generation of pagers using DI and config/services retrieved from the container.
