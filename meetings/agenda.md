# Next Technical Steering Committee Meeting Agenda

- Date: 2022-08-01
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Laminas Continuous Integration Actions

As of today, we do maintain `laminas-ci-matrix-action` and `laminas-continuous-integration-action` in separate repositories.
Every year, when a new PHP version comes out, both repositories needs changes so that the matrix will create jobs for the new PHP version and the action uses that new version when running jobs.

Since that is actually the main job of both actions (to be in sync when it comes to PHP versions), [Marco](https://github.com/Ocramius) suggested to merge both actions to the same repository so we can keep releases in sync.

[Max](https://github.com/boesing) is actually working on some kind of `before_script` logic which allows projects and the CI matrix action to provide commands which are executed before every command run.
This has to be first implemented in the `laminas-continuous-integration-action` before it can be added to the `laminas-ci-matrix-action` (or we need at least a synchronized release).

Lets gather some ideas on how this could look as we have to create dedicated releases per action. Having projects to update their workflows because we create a monorepo should be avoided.
