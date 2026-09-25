# Next Technical Steering Committee Meeting Agenda

- Date: 2026-10-05
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### PHP 8.6

PHP 8.6 is the next major release of PHP, scheduled for 19 November 2026.
We should discuss a solution for how we can carry out the update process without having to take people away from ongoing development work for weeks on end again.
Would an automated update process – for example, using Rector and other tools or processes – be a viable option, or would it make more sense to put together a team for this?

https://php.watch/versions/8.6/changelog

### Note PHPStorm Providing Licences Somewhere on the Website

Thanks to Julian Somesan for organising, we recently received Jet Brains licences for their all-products pack, certainly to me and possibly Xerkus.

It occurred to me that we should publicly acknowledge this on the website somewhere with a link back to the JetBrains website.

This should make it easier to request renewals and further licences for other team members in the future and at the very least is courteous!  

### Change Renovate config to *bump* dev deps instead of updating the lock

Can we discuss changing the strategy for our org-wide renovate configs to:

```json
{
    "$schema": "https://docs.renovatebot.com/renovate-schema.json",
    // .....
    "packageRules": [
        // ....
        {"matchDepTypes": ["require"], "rangeStrategy": "widen"},
        {"matchDepTypes": ["require-dev"], "rangeStrategy": "bump"}
    ]
    // .....
}
```
