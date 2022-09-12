# Next Technical Steering Committee Meeting Agenda

- Date: 2022-09-12
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Default git branching for new majors

When creating a new major, the relevant branch is created; it is also set as the default branch for the repository. However, there can be a significant gap between branch creation and the first release of that major version.

Contributors and renovate, will attempt to make bugfixes to this new major when they equally apply to the previous (current latest release) major.

I propose that the default branch should only be changed to the new major branch, once a release has been tagged for that new major.

### Security only packages and dependency updates

Is this intention for security only packages to eventually be abandoned? If no, then should we (I) look at ways to allow renovate to keep these up to date, if only to give us warning when the package may actually need maintenance. Currently any PR would be automatically closed, including the "Configure Renovate" PRs.

### Introduce Package to De-Couple `laminas-view` from `laminas-mvc`

@gsteel suggests creating a new package to act as a bridge between `laminas-mvc` and `laminas-view` so that as part of a 3.0 release, `view` can become independent of `mvc`.

The need for this package is immediately apparent in the way that certain helpers shipped with `view` are highly `mvc` specific such as the Url View Helper.

The ultimate goal is that `laminas-mvc-view` would become a hard dependency for `laminas-mvc` and `laminas-view` would not depend on `mvc` at all.

Relevant [RFC can be found here](https://github.com/laminas/technical-steering-committee/issues/123)… and work in progress on the proposed package is at [gsteel/laminas-mvc-view](https://github.com/gsteel/laminas-mvc-view/pull/1).

#### Questions:

- Is adding another package to the Laminas org acceptable? Or would it be preferable to add the code directly to `mvc`?
- There is a reasonable amount of configuration and factories etc inside `MVC` itself that could be hosted in the proposed package. Is it acceptable to extract code in MVC too, such as the various [View related factories](https://github.com/laminas/laminas-mvc/tree/4.0.x/src/Service)?
