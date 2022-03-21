# Next Technical Steering Committee Meeting Agenda

- Date: 2022-04-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss


### `laminas-view` v3.0 RFC

[Gary Lockett](https://github.com/internalsystemerror) filed an RFC for consideration in `laminas-view` [#149](https://github.com/laminas/laminas-view/issues/149) for an overall simplification of `laminas-view` that would include significant BC breaks for a number of related projects, possibly requiring new majors in those components too, for example `laminas-form` and `i18n`.
  By way of example, he opened [laminas/laminas-i18n#75](https://github.com/laminas/laminas-i18n/pull/75) that provides incremental changes to move towards compatibility with a 3.0 release of view.
  The overall goal of this 'simplification' is to make laminas-view as stateless as possible and appropriate for use outside of MVC: on the CLI, rendering email message views, running under Open/Swoole/React/Whatever without hidden state gotchas.

### Composer v1 support

[Maximilian Bösing](https://github.com/boesing) wants to get a decision on how to proceed with laminas/mezzio composer plugins and support for composer v1. As of https://github.com/laminas/laminas-component-installer/pull/46, composer v1 tests are executed for PHP 8.1 (wasn't the case prior this patch) and the tests were failing due to some incompatibility of composer v1 and phpunit reporting deprecations as exceptions. [Marco Pivetta](https://github.com/Ocramius) suggested to drop support for composer v1 entirely to get rid of the failing v1 tests.

To get a final decision here (as composer v1 received a release in january this year), we should talk about this in the TSC meeting.
