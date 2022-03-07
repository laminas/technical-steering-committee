# Next Technical Steering Committee Meeting Agenda

- Date: 2022-04-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

- [Gary Lockett](https://github.com/internalsystemerror) filed an RFC for consideration in `laminas-view` [#149](https://github.com/laminas/laminas-view/issues/149) for an overall simplification of `laminas-view` that would include significant BC breaks for a number of related projects, possibly requiring new majors in those components too, for example `laminas-form` and `i18n`.
  By way of example, he opened [laminas/laminas-i18n#75](https://github.com/laminas/laminas-i18n/pull/75) that provides incremental changes to move towards compatibility with a 3.0 release of view.
  The overall goal of this 'simplification' is to make laminas-view as stateless as possible and appropriate for use outside of MVC: on the CLI, rendering email message views, running under Open/Swoole/React/Whatever without hidden state gotchas.
