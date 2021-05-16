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

I prefer having `assert` over `@psalm-var` here, as it may fail in unit tests (or on non-production systems) and thus, the assertion will still be verified and not just assumed.

**Questions:**

- Do we want to use `assert` in some cases?
- If the answer to the first question was yes, how can we provide "rules" for doing so, so we can put these in the contributors guide?
- If the answer to the first question was no, do we want to require runtime `Assert` (webmozart) checks or do we accept inline `@psalm-var` annotations?
