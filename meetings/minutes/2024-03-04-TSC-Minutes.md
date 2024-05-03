# Minutes from the 2024-03-04 Laminas Technical Steering Committee Meeting

- When: 2024-03-04 at 19:00 UTC, until 21:06 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Gary Lockett
  - George Steel
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Maximilian Bösing
  - Michał Bundyra
  - Rob Allen

Quroum WAS met (13 out of 15 members were present).

## Agenda

### Discuss Issue [#164](https://github.com/laminas/technical-steering-committee/issues/164) - Communicating the status of components to users

[@visto9259](https://github.com/visto9259) raises a good [issue](https://github.com/laminas/technical-steering-committee/issues/164) on the TSC repository.
Effectively there is a lack of communication with users about the status of all components/libraries.

What can we do to improve the visibility of maintenance decisions for consumers?

#### Discussion

The first thing brought up was by Marco, who suggested we should interlink commits/issues/pull requests with the TSC meeting minutes where the decision was made.
This provides a trail for folks to explore to understand the status of a component.

Aleksei expanded on this, suggesting we create issues in security-only and similar repos and pin that issue.
The issue would reference the decision, giving us the linking Marco suggested.

Max suggested we do it as a status badge, as this would (a) be present in the repo, and (b) built into the docs.

Luís pointed out that while having issues and badges is helpful, it doesn't help with any effort to consolidate these statuses into an overview of _all_ packages.

George Steel suggested using GitHub's new [custom properties](https://github.blog/changelog/2023-10-12-github-repository-custom-properties-beta/) for this purpose.
These can be created at the organization level, with defaults, and there is an API for fetching them.

The main questions are:

- How can we make these statuses highly visible?
- How can we make it possible to retrieve these statuses programmatically?
- Can we accomplish both with one action, instead of requiring two changes per repository?

At this point, Aleksei, proposed:

- We manually create visible README notices
- We add custom properties to security-only repos:
  - `maintenance-status: security`
  - `maintenance-status-date: <Y-m-d>`
  - `maintenance-status-link: <link to minutes>`

With those in place, we can then later develop an action or other process to grab this information for a dashboard.

#### Decision

We will first update libraries to add a visible README notice if they are in security-only status.
Additionally, we will define custom properties with a "active" defaults for the maintenance status.
We will defer creation of a dashboard until these are in place.

Aleksei volunteered to do all work but dashboard creation for now.

### Marking ServiceManager as an optional dependency for components providing plugin managers 

Alexsei noted that right before the meeting, Michał opened an issue to make the ServiceManager optional for laminas-validator:

- https://github.com/laminas/laminas-validator/pull/232

He is worried that if we make it optional now, with SM version 4 having just dropped, the SM dependency won't be constrained by Composer, leading to conflicts.

Matthew suggested we mark SM v4 as a conflict in Composer.

Aleksei noted, however that optional dependencies have caused issues for us in the pat, and George and Andreas seconded that we should likely require dependencies if the symbol is used anywhere in the package — particularly when installing dev dependencies for developing the component.

Michał pointed out that the value had been in the `require-dev` section, but got moved to the `require` section without explanation during a minor version update.

Aleksei then pointed out that the problem isn't the proposal from Michał, but having the SM dependency optional at all, and it is pretty much in every component providing one.
Basically, even if we add a `conflict`, because the dependency was optional previously, Composer will just downgrade to a previous version where the conflict did not exist, and, because no conflict is present, install the _latest_ version of SM, even if it's not compatible with the plugin manager implementation.

This generated a lengthy discussion around optional dependencies, and what to do with components that declare plugin managers.
If we split the plugin manager out into its own component, existing users now need to _add_ that component for their own application to continue working correctly.
New users would need to likely add the plugin manager component as the primary dependency, inverting the expected installation path.
Additionally, we'd now have even _more_ packages to maintain going forward (though the plugin manager packages likely wouldn't change significantly).

Matthew pointed out that much of what the plugin managers do boils down to allowing usage of a "short name" for the individual plugins, and an array of options for configuration.
While the pattern works, it's easy to mis-spell option names or plugin names, and not get any valuable feedback when you do.
As such, it can be more solid to define an extension that configures itself in its constructor, and then pull that directly from the application service manager.
However, as George noted, this approach goes against usage of components like laminas-inputfilter or laminas-form, where creation often is defined via array shapes in configuration — an approach that provides a lot of value for users.
(But, as Gary noted, this can lead to the same issues that Matthew was pointing out; the utility of the array shapes is also its Achilles heel.)

At this point, we decided to defer a decision until we do more research into impact and alternative approaches.
(Max pointed out we could potentially make plugin manager registration work similarly to how laminas-cli defers command registration based on presence or absence of symfony/console.)
