# Next Technical Steering Committee Meeting Agenda

- Date: 2020-11-02
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

1. [RFCs - discuss directly on GitHub?](#rfcs---discuss-directly-on-github)
2. [Github Actions instead of Travis-CI?](#github-actions-instead-of-travis-ci)
3. [Laminas cache satellites to abandon](#cache-adapters-to-abandon)
4. [Commercial vendor program updates?](#commercial-vendor-program)

### Commercial vendor program updates?

Updates on the commercial vendor program? Any vote as appropriate?

### RFCs - discuss directly on GitHub?

As [noted by the user on the laminas slack](https://laminas.slack.com/archives/C4QBQUEG5/p1602604527127400), our current issue template suggests that
new features/RFCs should be posted to the forums for discussion.

That is quite inefficient, since:

 * the amount of users following the forum is a fraction of the users following our repositories
 * it is one more step for people to contribute

It could be a good idea to just endorse opening issues as "feature request" or "RFC" instead, since all the Laminas TSC members and community members
are quite familiar with PR/issue tooling of GitHub.

### Github Actions instead of Travis-CI?

Github Actions has been, so far, much faster and efficient to set up in repositories all over github.

While Travis-CI is certainly a good platform that has served us well for many many years, having the ability to create our own github actions may simplify
the CI setup for most our repositories.

The proposal is to:

 * Find an optimal "baseline" Github Actions workflow that we'd like to use
 * Investigate whether there is a way to unify most CI workflows (rather than maintaining them in each repository)
 * Move current Travis-CI configuration to Github Actions workflows
 * Sunset Travis-CI configuration and disable it on the various repositories


### Cache adapters to abandon

With `laminas/laminas-cache` v2.10, all cache adapters are moved to their own satellite.
Next step would be to abandon some of those packages as we are either dropping support for PHP <7.3 and some adapters never migrated to PHP 7 **or** we just dont want to support specific cache backends anymore.

The following adapters are currently "available":

- [APC](https://github.com/laminas/laminas-cache-storage-adapter-apc)
- [APCu](https://github.com/laminas/laminas-cache-storage-adapter-apcu)
- [BlackHole](https://github.com/laminas/laminas-cache-storage-adapter-blackhole)
- [DBA](https://github.com/laminas/laminas-cache-storage-adapter-dba)
- [ExtMongodb](https://github.com/laminas/laminas-cache-storage-adapter-ext-mongodb)
- [Filesystem](https://github.com/laminas/laminas-cache-storage-adapter-filesystem)
- [Memcache](https://github.com/laminas/laminas-cache-storage-adapter-memcache)
- [Memcached](https://github.com/laminas/laminas-cache-storage-adapter-memcached)
- [Memory](https://github.com/laminas/laminas-cache-storage-adapter-memory)
- [ExtMongodb](https://github.com/laminas/laminas-cache-storage-adapter-mongodb)
- [Redis](https://github.com/laminas/laminas-cache-storage-adapter-redis)
- [Session](https://github.com/laminas/laminas-cache-storage-adapter-session)
- [WinCache](https://github.com/laminas/laminas-cache-storage-adapter-wincache)
- [XCache](https://github.com/laminas/laminas-cache-storage-adapter-xcache)
- [ZendServer](https://github.com/laminas/laminas-cache-storage-adapter-zend-server)


#### We should abandon the following packages:

- APC 
    - it is superseded by APCu and thus not needed anymore
- Memcache 
    - it was dead for almost 7 years
    - Last year, some guys fixed the extension to work with PHP 7+ but its not in active development
- WinCache 
    - Windows (Microsoft dropped support for PHP anyways) 
    - there is no-one who can execute tests for this package (not even travis)
- XCache
    - is dead for years
    
- ZendServer
    - there is no-one who can execute tests for this package (not even travis)
