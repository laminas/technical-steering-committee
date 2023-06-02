# Next Technical Steering Committee Meeting Agenda

- Date: 2023-06-05
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Feasibility of adding RectorPHP to our workflow

RectorPHP has been used to assist with upgrading PHP versions in projects for some time and is closing on a 1.0 release.
Gary Lockett created a test PR for `laminas/laminas-diactoros` at https://github.com/laminas/laminas-diactoros/pull/163
in order to start gathering some feedback.

As a result Gary would like to discuss adding Rector to our workflow, whether it is feasible, worthwhile, and what our
intentions would be with such a tool. The basic proposal would be that we add it to check for any instances of PHP code
which can now be improved in newer versions, and automating that task.
