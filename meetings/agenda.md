# Next Technical Steering Committee Meeting Agenda

- Date: 2021-05-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

### Branch protection

[Filippo Tessarotto](https://github.com/Slamdunk) asks to add branch protection for release branches, see https://github.com/laminas/technical-steering-committee/issues/71


### Abandoning laminas-cache satellites (part 2)

[Maximilian Bösing](https://github.com/boesing) is working on `laminas-cache` to integrate new GHA workflow but has problems with some storage adapters due the fact that these are not maintainable at all. The TSC did already voted about this [back in november 2020]([jump to discussion](#cache-adapters)) but the vote was not focussing the abandoning and thus it is brought up again.

  `laminas-cache-storage-adapter-apc` can be safely abandoned with the hint that `laminas-cache-storage-adapter-apcu` is replacing it. The APC extension wont be available for PHP 8.0 as well and thus, abandoning/archiving it is the logical consequence.

  `laminas-cache-storage-adapter-memcache` - well, that was mentioned back in november 2020, as it was not actively developed. As it received a bump to 8.0 in december 2020 to support PHP 8.0+, we should keep it (sadly, `memcached` extension cannot catch up as it is still not released for PHP 8.0).

  Given the fact, that `zend-server` is a paid product, there is no way of providing maintenance from within the laminas project. As there were discussions of adding perforce employees as maintainers for `laminas-db`, the `laminas-cache-storage-adapter-zend-server` component might be interesting for them aswell. If not, Max' intention is to mark the adapter as abandoned/archived.

  `laminas-cache-storage-adapter-xcache` is another adapter which is unmaintainable. `Xcache` ([Wikipedia](https://de.wikipedia.org/wiki/XCache)) was developed in 2006 until 2014 (atleast Wikipedia says there was the `3.2.0` release). Even their website gives us 404 and thus, we should abandon and archiving it.

  `laminas-cache-storage-adapter-mongodb` is another adapter which is unmaintainable. [`ext-mongo`](https://pecl.php.net/package/mongo) is not officially available for PHP 7 and not available at all in ondrej apt packages.

  Last, but not least: `laminas-cache-storage-adapter-wincache`. The `wincache` adapter is windows only and due to the fact, that the new GHA workflow does not support PHP on Windows and Microsoft stopped supporting PHP for Windows ([internals](https://news-web.php.net/php.internals/110907)), we should drop support for `wincache` as well and mark the component as abandoned/archived.

  Having these adapters removed will help spending time on those adapters which we can actively support along with proper integration tests within our CI pipeline.

### Contribution guidelines

[Maximilian Bösing](https://github.com/boesing) already requested internally on how we can make the [CONTRIBUTING.md](https://github.com/laminas/.github/blob/17209d8266a487fbe280d9fac63f63f1b5e43157/CONTRIBUTING.md) and the [CODE_OF_CONDUCT.md](https://github.com/laminas/.github/blob/361a092443d78d33b0f0445bfe4b1ac8e93efc85/CODE_OF_CONDUCT.md) more visible in the components.

At the moment, these files are hidden in the community part (when hitting Insights).
1. Open https://github.com/laminas/.github/
2. Click on "Insights"
3. Click on "Community"
4. Click on either "Contributing" or "Code of Conduct"

Another way of being pointed to these files is under each `textarea` (e.g. when creating/commenting on issues/PRs). 
There is a tiny text: `Remember, contributions to this repository should follow its contributing guidelines and code of conduct.`

----

There are projects which have these files directly stored in all of their components but that is not an option due to the fact that changing these files would need changes in **all** packages.

[Matthew](https://github.com/weierophinney) mentioned, that we could add a `Contributors` section on the website.
[Frank](https://github.com/froschdesign) came up with the idea of linking to these files from within the `README.md`.

Frank will make a suggestion in form of a pull request for the `Contributors` section on the website.

**Questions**
Do we want to add links to the `CONTRIBUTORS` and the `CODE_OF_CONDUCT` to the `README.md` of all packages?
Is there a way of creating **and** merging PRs from CLI for Markdown changes like these? 
There should be no need to release this as a new version of the package so merging this to the default branch would be enough, right?  
