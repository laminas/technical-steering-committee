# Next Technical Steering Committee Meeting Agenda

- Date: 2021-06-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Remove Line Length Limit from Codestandard

[Maximilian Bösing](https://github.com/boesing) wants to drop the line length limit from the `laminas-codestandard` ruleset.

The line length limit is counter-productive in combination with psalm and more precise argument-/return-type definitions.

### Allow PHP-Assert along with Webmozart-Assert in Specific Cases

[Maximilian Bösing](https://github.com/boesing) wants to talk about the usage of `assert` (PHP) and `Assert` (Webmozart) when providing types for psalm.
In some cases, having runtime assertions may consume unnecessary opcodes just to provide proper psalm-types.

Lets assume the following code:

```php
$foo = sprintf('foo bar baz %d', 1);
assert($foo !== '');
```

Psalm is not able to verify that `$foo` is a non-empty-string, even tho, the first argument is a non-empty string and therefore, the return value must either be `false` (in case of an error) or `non-empty-string`.

https://psalm.dev/r/add6e2b321

I prefer using `assert($foo !== '')` over `Assert::stringNotEmpty` to avoid redundant runtime checks which actually only have to be made to "make psalm happy".
As I do want to "make psalm happy", I can either use the `@psalm-var` inline-annotation, use `assert` or use `@psalm-assert` (as provided by webmozart `Assert`).

The first two options do not execute runtime checks (`assert` won't on production system as `zend.assertion` supposed to be `-1`). The webmozart assertion will execute assertions even tho the assertion will always succeed.

Note that `zend.assertion` should be changed for CI to `1` as by default it's `-1` in `laminas-continuous-integration-action` too, see https://github.com/laminas/laminas-continuous-integration-action/issues/36.

I prefer having `assert` over `@psalm-var` here, as it may fail in unit tests (or on non-production systems) and thus, the assertion will still be verified and not just assumed.

**Questions:**

- Do we want to use `assert` in some cases?
- If the answer to the first question was yes, how can we provide "rules" for doing so, so we can put these in the contributors guide?
- If the answer to the first question was no, do we want to require runtime `Assert` (webmozart) checks or do we accept inline `@psalm-var` annotations?

### Locked Dependencies for All Supported PHP Versions

[Maximilian](https://github.com/boesing) wants to talk about the current CI matrix.
Lately, we encountered some issues with different 3rd party libraries due to the fact that these are way more strict in dropping PHP versions along with major bumps.

This makes it almost impossible to have a `composer.lock` which will be valid for **all** PHP versions (`7.3`, `7.4`, `8.0` so far).

Some packages where it would be impossible to have a proper `composer.lock` for all supported versions (without dropping support for these versions and/or swapping to alternatives):

| Package | Major Version | PHP constraint
|---------|------------|--------
| [maglnet/composer-require-checker](https://github.com/maglnet/ComposerRequireChecker) | 2.x | `^7.2`
| [maglnet/composer-require-checker](https://github.com/maglnet/ComposerRequireChecker) | 3.x | `^7.4 \|\| ^8.0`
| [ocramius/package-versions](https://github.com/Ocramius/PackageVersions/) | 1.5.1 | `^7.3`
| [ocramius/package-versions](https://github.com/Ocramius/PackageVersions/) | 2.0 | `^7.4.7`
| [ocramius/package-versions](https://github.com/Ocramius/PackageVersions/) | 2.1 | `^7.4.7 \|\| ~8.0.0`

For `ocramius/package-versions` we already had to switch to `composer/package-versions-deprecated` to get some of our components up and running with the current matrix.
That's all due to the fact that we need one single `composer.lock` to fit for all PHP versions.
This will become more and more a problem when projects start to drop old PHP versions.

So we have two options:

1. drop support of PHP version as soon as 3rd-party libraries we are using drop support for these versions
1. only use `locked` dependencies for the stable version marked by the `dev.laminas.org` API which is requested in the matrix generation(?) and for all other versions, use `lowest` or `latest`

The latter will work with the [recent suggestions](https://gist.github.com/weierophinney/b003e50c3c2667d08076caf31ebd36a4) of [Matthew](https://github.com/weierophinney) regarding the migration to GHA.
That guide says:

> Using PHP 7.4, run composer update

So even tho, the component had support for PHP 7.3, some packages might be ended up having a `.laminas-ci.json` with these contents:

```json
{
    "exclude": [
        {"name": "PHPUnit on PHP 5.6 with locked dependencies"},
        {"name": "PHPUnit on PHP 7.0 with locked dependencies"},
        {"name": "PHPUnit on PHP 7.1 with locked dependencies"},
        {"name": "PHPUnit on PHP 7.2 with locked dependencies"}
    ]
}
```

This said, there should be no reason why we need `locked` dependencies for all PHP versions.

### Enable Coveralls support in laminas-continuous-integration-action

The switch from Travis to Github Actions has seen Coveralls support not ported.

[Filippo Tessarotto](https://github.com/Slamdunk) ask to re-enable it: having the code-coverage
feedback automation is a great value and help for maintainers to evaluate Pull-Requests validity.
