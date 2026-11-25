# Next Technical Steering Committee Meeting Agenda

- Date: 2026-12-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Move laminas-cache-storage-deprecated-factory to Security-Only Maintenance Mode

This component is declared as a temporary solution:

> Temporary storage adapter factory for fluent migration to laminas-cache v3 when working with laminas components which depend on laminas-cache

Nobody has asked for support to be added for PHP 8.5, and I don’t expect this to be the case for 8.6 either.
Therefore, we should move it to security-only maintenance mode.
(I wouldn’t mark it as deprecated, as we haven’t yet reached the point where version 4 of laminas-servicemanager is supported [in all related components](https://github.com/laminas/laminas-servicemanager/issues/216).)
