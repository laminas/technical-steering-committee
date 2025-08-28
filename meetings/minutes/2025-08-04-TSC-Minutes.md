# Minutes from the 2025-08-04 Laminas Technical Steering Committee Meeting

- When: 2025-08-04 at 19:00 UTC, until 20:12 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Frank Brückner
    - George Steel
    - James Titcumb
    - Julian Somesan
    - Michał Bundyra
    - Rob Allen

Quorum WAS NOT met (6 out of 16 members were present).

## Agenda

### New Quick Start Guide for Mezzio

We need to create a new Quick Start Guide for Mezzio, as the current one is outdated and does not reflect the latest changes in the framework.
The new guide should be user-friendly to provide a good starting point for new users, and later be expanded with more tutorials.

#### Discussion

George and Rob were in favor of extending the documentation, which can lead to smoother onboarding, with guides on how to start on a new project.
Julian mentioned there are already 2 articles in the Mezzio 101 series and more can be added.

#### Decisions

Frank offered to start a new GitHub project and add ideas as issues for new items in the guide.

### Mark MVC Related Libraries as Security-Only in line with `laminas-mvc`

This refers to the MVC packages that are still in active maintenance and should be in security-only, like `laminas-mvc`:

- laminas-developer-tools
- laminas-mvc-form
- laminas-mvc-i18n
- laminas-mvc-middleware
- laminas-mvc-plugin-fileprg
- laminas-mvc-plugin-flashmessenger
- laminas-mvc-plugin-identity
- laminas-mvc-plugin-prg
- laminas-mvc-plugins
- laminas-mvc-view (un-released)
- laminas-test
- laminas-mvc-skeleton
- laminas-modulemanager
- laminas-config-aggregator-modulemanager
- laminas-skeleton-installer
- laminas-composer-autoloading

#### Decisions

The poll confirmed that the packages should receive the status update to security-only, with the side-note that the unreleased `laminas-mvc-view` should be archived.

### Mezzio charting a new visual direction

The item is based off [this RFC](https://github.com/laminas/getlaminas.org/issues/298).
The PFD presentation includes 3 logos that the members can vote on.

#### Discussion

Julian mentioned that the current Laminas logo should be kept as is, with only the Mezzio logo in discussion.
The new Mezzio logo needs to be easily recognizable, since it will be used on promotional material (stickers, t-shirts etc.).

George, James, Julian and Rob weighed in on the 3 logos.
Some appreciated the new design choices, while others preferred to keep some history in the new logo (like in the 2nd wavy logo).

#### Decisions

A poll was created, and it passed on the following day, with the 1st logo (tilted 3-stripes) being chosen.

### Going live with Laminas Integrations page

This item is based off a [RFC](https://github.com/laminas/getlaminas.org/pull/226) and [Instruction about how to propose a package](https://github.com/laminas/getlaminas.org/blob/preview-1/ADD_INTEGRATION.md).

#### Discussion

Tyrsson (Joey Smith) mentioned that there are items in the integrations page that can't be assigned to the currently available categories.
Julian replied that there is no reason not to submit his own packages, since the category dropdown is removed.
George recommended that the page should list more items/page (18 instead of 9) and receive a few design changes.

#### Decisions

Since there are no other blockers, the members were in favor of pushing the page live.

### Release `laminas-view` v3.0.0

George is ready with the core code.
Only the View Model interface, its implementation, and the overall documentation update are open.

#### Discussion

George asked for the poll on release `laminas-view` to see if other members have anything to add for the core code.
Julian mentioned that the release will impact current projects that may need refactoring and other packages like `laminas-inputfilter`, `laminas-session`.
George also added `mezzio-laminasviewrenderer`, `laminas-form` and `laminas-i18n` that would be impacted.

#### Decisions

A poll was created, and it passed in favor of releasing the package.

The following TSC meeting falls on September 1st, but it may be moved to the 8th because of Labor Day.