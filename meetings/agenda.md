# Next Technical Steering Committee Meeting Agenda

- Date: 2022-09-12
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Default git branching for new majors

When creating a new major, the relevant branch is created; it is also set as the default branch for the repository. However, there can be a significant gap between branch creation and the first release of that major version.

Contributors and renovate, will attempt to make bugfixes to this new major when they equally apply to the previous (current latest release) major.

I propose that the default branch should only be changed to the new major branch, once a release has been tagged for that new major.

### Security only packages and future updates

Is this intention for security only packages to eventually be abandoned? If no, then should we (I) look at ways to allow renovate to keep these up to date, if only to give us warning when the package may actually need maintenace. Currently any PR would be automatically closed, including the "Configure Renovate" PRs.
