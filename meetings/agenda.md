# Next Technical Steering Committee Meeting Agenda

- Date: 2025-02-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Major release for laminas-session

    In order to implement servicemanager v4, we need to release a new major version, V3, of this laminas-session package.
    See those PR's: https://github.com/laminas/laminas-session/pull/102  and https://github.com/laminas/laminas-session/pull/103

    In the current bugfix release, all functions that will be removed in V3 was marked as `@deprecated`.

### Email accounts @getlaminas.org 

    In the past we were looking for email providers, and we should discuss if this Tuta solution works for us.
    
     https://tuta.com/blog/tutanota-for-open-source-teams
    
### Dropping Support for PHP 8.1

@gsteel wants to, as a general rule, drop support for PHP 8.1 so that as we upgrade to Psalm v6, we can also Upgrade to PHPUnit 11 at the same time. This will help keep our dev dependencies healthy and improve quality over time.

Any objections?

### New design and layout

    Based on the current visual identity , @arhimede is proposing a new design and improved layout. 
    https://github.com/laminas/getlaminas.org/issues/242
