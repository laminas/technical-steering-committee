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
