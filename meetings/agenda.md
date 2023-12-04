# Next Technical Steering Committee Meeting Agenda

- Date: 2023-12-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Maintainers for laminas-mime and laminas-mail

Slamdunk and settermjd have offered to maintain laminas-mime and laminas-mail; should we approve this, or mark laminas-mail as a security only package?

### BC Checks in the CI pipeline

Slamdunk requests that we add [roave/BackwardCompatibilityCheck](https://github.com/Roave/BackwardCompatibilityCheck) as a default job to be run in CI.

### Pimple service manager configuration

Should we abandon [laminas/laminas-pimple-config](https://github.com/laminas/laminas-pimple-config)?

- [Last release was in October 2021](https://github.com/silexphp/Pimple/tags)
- [Package stats laminas-pimple-config](https://packagist.org/packages/laminas/laminas-pimple-config/stats)
- Frank notes that the project is abandoned, and we could just mark ours as "security-only"; however, once we reach the last PHP version supported by Pimple, we may still need to abandon it.

### PHPCS is being abandoned/forked

For more context, [see this issue](https://github.com/squizlabs/PHP_CodeSniffer/issues/3932) by [@jrfnl](https://github.com/jrfnl), which effectively announces the fork and the probable (?) abandonment of the source package.

[Slevomat CS has indicated they will switch to the fork](https://github.com/slevomat/coding-standard/issues/1640). 
