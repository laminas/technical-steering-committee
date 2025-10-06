# Next Technical Steering Committee Meeting Agenda

- Date: 2025-10-06
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Release v3 of `mezzio-template`

There's 1, simple [outstanding PR](https://github.com/mezzio/mezzio-template/pull/41) to merge and then `mezzio-template@3.0.0` is ready to release.

There's not much to talk about, main details in the [milestone for v3](https://github.com/mezzio/mezzio-template/milestone/4)

### Release v3 of `mezzio-laminasviewrenderer`

Whilst release of this lib is contingent on the release of `laminas-view@v3` and `mezzio-template@v3`, it is effectively "good to go" once a couple of outstanding PRs are merged. It makes sense to take a vote now rather than next month, so that it can be released ASAP once the upstream deps are released.

- [3.0.0 Milestone](https://github.com/mezzio/mezzio-laminasviewrenderer/milestone/3)

### Adding 8.5 Support Everywhere…

Now that 8.5 is available in CI _(Currently RC 1)_ it is feasible to start testing on 8.5 anywhere it makes sense to add support for PHP 8.5

8.1 will be [EOL at the end of 2025](https://www.php.net/supported-versions.php).

Should we make it policy drop 8.1 support at the same time as adding 8.5 support, even though there are a couple of months of security support left? Or, should we retain 8.1 support until it subjectively or objectively starts causing a maintenance burden?

### Attending the Dutch PHP Conference

Does it worth to sponsor a small booth space at [The Dutch PHP conference](https://phpconference.nl/) ?

It is one of the few major European PHP general conferences (not Laravel or Symfony).

If yes, how we can find the funds for a [Silver option](https://webdevcon.nl/sponsors/packages/#showTable), to have a small booth there ?

### Adopt PER Coding Style

PSR-12 coding standard was introduced 6 years ago and does not cover new PHP
features released since. Our own coding standard is an extension to PSR-12.
Our own rules narrow down PSR-12 and also address some of the new feautures.

PER Coding Style, currently at the version 3.0, is an *evolving* standard
that keeps up with the PHP releases and aims to remain compatible with PSR-12 when
practical but does not guarantee it.

In terms of adoption as of now we would gain new rules addressing what was not
covered by our standard as well as rules that simply make our additions
redundant.

Some of the topics covered by the new rules are compound types, short
closures, attributes, enums, old and new modifier keywords including assymetric visibility
for properties, constructor property promotion, property hooks. multi-line operators placement.

Preliminary changes can be viewed as a diff here https://github.com/laminas/laminas-coding-standard/pull/93/files?diff=split

With the decision to adopt PER Coding Style our coding standard would switch to and
track latest version of the evolving recommendation. Should our extended rules
conflict with the newer versions, PER CS would win.
