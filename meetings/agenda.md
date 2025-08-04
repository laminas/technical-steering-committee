# Next Technical Steering Committee Meeting Agenda

- Date: 2025-08-04
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

The libs proposed are the following:

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

The un-released `laminas-mvc-view` should likely be abandoned and archived. No releases have been made, and it has not been published on Packagist.

### Discussion related to Laminas Ecosystem 

Preview is here [Laminas Ecosystem](https://preview-1-hy2vwsq-2ja7ciew2nbkm.us-2.platformsh.site/ecosystem/)
- What if we remove from **Usage** drop-down the MVC, and keep only middleware? Or remove that drop-down completely ?
- The design of this page still needs some improvements. @froschdesign 
- In the corresponding [RFC](https://github.com/laminas/getlaminas.org/pull/226)  there are various opinions, not sure which direction to follow 

### Release `laminas-view` v3.0.0

Code changes for Laminas View are complete except some miscellaneous clean up required in the View Model interface and implementation, and, work on documentation. If possible, a vote on its release based on the current source would be desirable.

Once the remaining work is complete, I'd like to release ASAP so that we can start working on other components that depend on view such as i18n.

[v3.0.0 Milestone](https://github.com/laminas/laminas-view/milestone/1)
