# Next Technical Steering Committee Meeting Agenda

- Date: 2026-08-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Consider Adopting Mago in place of Psalm and PHP_CodeSniffer

I've sent in a patch to `laminas-validator` ([#476](https://github.com/laminas/laminas-validator/pull/476)) to illustrate some of the changes involved.

Discussion points

- Performance. Mago runs (for any of lint, analyse and format) at sub-second speeds. This is incomparably faster than our current tooling
- Formatting. Using the default PER-CS standard, there is very little difference to our existing CS rules, the diff was [pretty small for validator](https://github.com/laminas/laminas-validator/pull/476/changes/2d8bb091d7c9b4fe51f82ec0b75d7bac6bb65724), and required just a few minor config tweaks.
- Mago is very actively developed, it's getting more traction, and tooling support is getting better all the time. Specifically, mago is supported by infection where the current psalm support in infection looks a bit doomed from v7 (un-released) onwards (the Roave SA plugin maintained by Marco is not looking likely to get v7 support).
- Dependency management. Mago, when installed via composer is dependency free, so no more dependency upgrade difficulties with tooling.
- Configuration… takes some effort to learn, but does have a well-defined schema. We can also ship mago config as a composer dependency org-wide and use `extends =` to provide default, org-wide configuration.
- We currently have no support for mago in the CI matrix, we could probably run mago out of the `additional_checks` key for the Laminas CI action instead of adding the runs directly to GHA config.
- A new major release of Psalm is possibly coming soon. The work required to get Psalm upgrading is not likely to be dissimilar to switching to mago I'd estimate.
- It's possible that Mago v2 could be a painful upgrade, at least from CI configuration as I believe the lint and analyse tools may be getting merged and there is also talk of introducing levels (as per PHPStan / Psalm)

### Allow compatible Rector versions for `laminas-servicemanager-migration`

As I’m now less involved in Rector’s day-to-day development and verification, I may not always be available to review and validate every Rector dependency update for this package.

Because of that, I’m wondering whether we could replace the pinned version in:

* https://github.com/laminas/laminas-servicemanager-migration

with a compatible version constraint:

```diff
-"rector/rector": "2.5.7"
+"rector/rector": "^2.5.7"
```

This would allow compatible Rector updates without requiring a separate pull request for every release. We could then remove the related Renovate `rangeStrategy` configuration from `renovate.json`.

When a future Rector release introduce an incompatible API change, we can address it when needed.
