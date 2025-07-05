# Next Technical Steering Committee Meeting Agenda

- Date: 2025-07-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### New Quick Start Guide for Mezzio

We need to create a new Quick Start Guide for Mezzio, as the current one is outdated and does not reflect the latest changes in the framework.
The current guide is not user-friendly and does not provide a good starting point for new users.  
Later we can add more tutorials like we have for laminas-mvc, but first we need to have a good starting point.

Some ideas for the new guide:

- Use CLI commands to create the application with request handlers, middleware, routes, and templates
- Add images, animations, and/or videos to make it more engaging
- Allow Docker as an alternative (https://github.com/mezzio/mezzio-skeleton/pull/165)
- Implement roave/psr-container-doctrine (https://github.com/Roave/psr-container-doctrine)
- Replace Bootstrap with a minimal CSS framework (e.g., [Pico CSS](https://picocss.com))
- …

The following items need to be addressed:

- Update the skeleton application
- Extend the command line tooling with more commands and easier usage (select options by arrow keys, etc.)
- Create a complete new guide which uses the new skeleton application and the new command line tooling

New helpers may be required to issue flash messages, enable access to the authentication identity or something similar.

### Mark MVC Related Libraries as Security-Only in line with `laminas-mvc`

According to the [maintenance overview](https://getlaminas.org/packages-maintenance-status/), MVC has already been marked as `security-only`, but the other MVC specific libs are still in active maintenance.

George proposes _(And volunteers)_ to update the attributes/labels on these repos to security only mode, i.e. `mvc-form`, `mvc-plugin-prg` etc…
