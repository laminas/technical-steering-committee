# Next Technical Steering Committee Meeting Agenda

- Date: 2021-05-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

### Branch protection

[Filippo Tessarotto](https://github.com/Slamdunk) asks to add branch protection for release branches, see https://github.com/laminas/technical-steering-committee/issues/71


### Abandoning laminas-cache satellites (part 2)

[Maximilian Bösing](https://github.com/boesing) is working on `laminas-cache` to integrate new GHA workflow but has problems with some storage adapters due the fact that these are not maintainable at all. The TSC did already voted about this [back in november 2020](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2020-11-02-TSC-Minutes.md#cache-adapters) but the vote was not focussing the abandoning and thus it is brought up again.

  `laminas-cache-storage-adapter-apc` can be safely abandoned with the hint that `laminas-cache-storage-adapter-apcu` is replacing it. The APC extension wont be available for PHP 8.0 as well and thus, abandoning/archiving it is the logical consequence.

  `laminas-cache-storage-adapter-memcache` - well, that was mentioned back in november 2020, as it was not actively developed. As it received a bump to 8.0 in december 2020 to support PHP 8.0+, we should keep it (sadly, `memcached` extension cannot catch up as it is still not released for PHP 8.0).

  Given the fact, that `zend-server` is a paid product, there is no way of providing maintenance from within the laminas project. As there were discussions of adding perforce employees as maintainers for `laminas-db`, the `laminas-cache-storage-adapter-zend-server` component might be interesting for them as well. If not, Max' intention is to mark the adapter as abandoned/archived.

  `laminas-cache-storage-adapter-xcache` is another adapter which is unmaintainable. `Xcache` ([Wikipedia](https://de.wikipedia.org/wiki/XCache)) was developed in 2006 until 2014 (atleast Wikipedia says there was the `3.2.0` release). Even their website gives us 404 and thus, we should abandon and archiving it.

  `laminas-cache-storage-adapter-mongodb` is another adapter which is unmaintainable. [`ext-mongo`](https://pecl.php.net/package/mongo) is not officially available for PHP 7 and not available at all in ondrej apt packages.

  `laminas-cache-storage-adapter-dba` is quite tough. The CI pipeline was never covering all supported [DBA handlers](https://www.php.net/manual/en/dba.installation.php) and thus, maintenance is a burden as well. To support all these handlers, we need to compile PHP per supported version (`7.3`, `7.4`, `8.0` as of now) with all available handlers (`dbm`, `ndbm`, `gdbm`, `db2`, `db3`, `db4`, `cdb`, `flatfile`, `inifile`, `qdbm`, `tcadb`, `lmdb` as of now). The matrix would be hilariously huge just to cover all handlers. Well, some of them work together, but at least all those `dbX` handlers are conflicting each other. So in the end, supporting all handlers of the `dba` extension is unacceptable so we should abandon and archive this as well. 

  Last, but not least: `laminas-cache-storage-adapter-wincache`. The `wincache` adapter is windows only and due to the fact, that the new GHA workflow does not support PHP on Windows and Microsoft stopped supporting PHP for Windows ([internals](https://news-web.php.net/php.internals/110907)), we should drop support for `wincache` as well and mark the component as abandoned/archived.

  Having these adapters removed will help spending time on those adapters which we can actively support along with proper integration tests within our CI pipeline.
