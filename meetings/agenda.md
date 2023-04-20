# Next Technical Steering Committee Meeting Agenda

- Date: 2023-05-08
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

### DotKernel members' contribution to Laminas/Mezzio packages
Since the last TSC (April 2023), DotKernel members started creating PRs to various Laminas/Mezzio packages.

See a couple of examples:
- https://github.com/mezzio/mezzio-session-ext/pull/48
- https://github.com/mezzio/mezzio-hal/pull/78
- https://github.com/mezzio/mezzio/pull/151

Most of our PRs fail due to the latest modifications introduced in PHPUnit:
- `PHPUnit [8.x, lowest]` checks **pass**
- `PHPUnit [8.x, locked]` checks **pass**
- `PHPUnit [8.x, latest]` checks **fail** because currently the latest version of PHPUnit is 10.1.x, which contains BC breaks

Our suggestions for the `PHPUnit [8.x, latest]` check:
- temporarily limit PHPUnit to version 10.0.*
- temporarily disable this check, until PHPUnit sorts this out on their end
