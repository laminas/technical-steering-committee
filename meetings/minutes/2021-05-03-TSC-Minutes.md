# Minutes from the 2021-05-03 Laminas Technical Steering Committee Meeting

- When: 2021-05-03 at 19:00 UTC, until 20:21 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brückner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Max Bösing
  - Rob Allen

Quorum was met (10 out of 16 members were present).

## Agenda

### Branch Protection

[Filippo Tessarotto](https://github.com/Slamdunk) asks to add branch protection for release branches, see https://github.com/laminas/technical-steering-committee/issues/71

---

[Matthew](https://github.com/weierophinney) asked why Filippo felt this would be a neccesary and/or good practice, to which the answer was "humans make a lot of mistakes, [branch protection] prevents dangerous one[s] at cheap cost."
[Rob](https://github.com/akrabat) asked if it would affect any of our release automation; the answer here is no, as we only ever push new changes to a branch, or create new release branches, but never force push.
Rob then asked if this would prevent who could create new branches; Matthew noted that the default is just to disable force pushes, and that any additional limits have to be configured specifically.
[Max](https://github.com/boesing) asked if this would affect new forks of our repositories - if they would inherit the settings, and thus prevent users from force-pushing their own branches (which is common when updating pull request branches).
[Aleksei](https://github.com/xerkus) notes that forks do not inherit branch protection settings.
The main concern raised at this point is that branch protection does not prevent erroneous commits from entering _newly created_ branches.
However, we've found that manual branch creation primarily happens when a major release branch has been created, and a new minor on the previous major series is needed.
It's rare, and likely to become more rare going forward.

Finally, Aleksei pointed out that we can provide patterns to match branch names against when applying branch protection, which would allow us to limit it only to release branches.

We proceeded to a vote; all present voted in favor, giving us greater than our required majority.
The vote passed.
We will begin enabling branch protections on repositories.

### Abandoning Laminas-Cache Satellites (Part 2)

[Maximilian Bösing](https://github.com/boesing) is working on `laminas-cache` to integrate new GHA workflow but has problems with some storage adapters due the fact that these are not maintainable at all. The TSC did already voted about this [back in november 2020](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2020-11-02-TSC-Minutes.md#cache-adapters) but the vote was not focussing the abandoning and thus it is brought up again.

`laminas-cache-storage-adapter-apc` can be safely abandoned with the hint that `laminas-cache-storage-adapter-apcu` is replacing it. The APC extension wont be available for PHP 8.0 as well and thus, abandoning/archiving it is the logical consequence.

`laminas-cache-storage-adapter-memcache` - well, that was mentioned back in november 2020, as it was not actively developed. As it received a bump to 8.0 in december 2020 to support PHP 8.0+, we should keep it (sadly, `memcached` extension cannot catch up as it is still not released for PHP 8.0).

Given the fact, that `zend-server` is a paid product, there is no way of providing maintenance from within the laminas project. As there were discussions of adding perforce employees as maintainers for `laminas-db`, the `laminas-cache-storage-adapter-zend-server` component might be interesting for them as well. If not, Max' intention is to mark the adapter as abandoned/archived.

`laminas-cache-storage-adapter-xcache` is another adapter which is unmaintainable. `Xcache` ([Wikipedia](https://de.wikipedia.org/wiki/XCache)) was developed in 2006 until 2014 (atleast Wikipedia says there was the `3.2.0` release). Even their website gives us 404 and thus, we should abandon and archiving it.

`laminas-cache-storage-adapter-mongodb` is another adapter which is unmaintainable. [`ext-mongo`](https://pecl.php.net/package/mongo) is not officially available for PHP 7 and not available at all in ondrej apt packages.

`laminas-cache-storage-adapter-dba` is quite tough. The CI pipeline was never covering all supported [DBA handlers](https://www.php.net/manual/en/dba.installation.php) and thus, maintenance is a burden as well. To support all these handlers, we need to compile PHP per supported version (`7.3`, `7.4`, `8.0` as of now) with all available handlers (`dbm`, `ndbm`, `gdbm`, `db2`, `db3`, `db4`, `cdb`, `flatfile`, `inifile`, `qdbm`, `tcadb`, `lmdb` as of now). The matrix would be hilariously huge just to cover all handlers. Well, some of them work together, but at least all those `dbX` handlers are conflicting each other. So in the end, supporting all handlers of the `dba` extension is unacceptable so we should abandon and archive this as well.

Last, but not least: `laminas-cache-storage-adapter-wincache`. The `wincache` adapter is windows only and due to the fact, that the new GHA workflow does not support PHP on Windows and Microsoft stopped supporting PHP for Windows ([internals](https://news-web.php.net/php.internals/110907)), we should drop support for `wincache` as well and mark the component as abandoned/archived.

Having these adapters removed will help spending time on those adapters which we can actively support along with proper integration tests within our CI pipeline.

---

After receiving a synopsis from Max, Matthew notes that Perforce can likely take the zend-server adapter in-house for its customers.
Rob asked about the mongo extension, and was reminded by Max that it became mongdb for PHP 7, and laminas-cache only supports PHP 7 releases at this time.

Aleksei notes that the various dba adapters might be of interest to IBM i users; Matthew points out that with the modern Open Source Environment available to that platform, they have a lot of new and better capabilities, including Redis, available to them.
Filippo noted that since adapters have been split to satellite packages already anyways, it will be easy to re-add them later, or for somebody to offer and maintain their own adapters if desired.

We immediately moved to a vote, with, again, a unanimous outcome to accept Max's proposal.
We will archive the APC (but not APCu), memcache (but not memcached), xcache, mongo (but not mongodb), dba, and wincache adapters.

### Contribution Guidelines

[Maximilian Bösing](https://github.com/boesing) already requested internally on how we can make the [CONTRIBUTING.md](https://github.com/laminas/.github/blob/17209d8266a487fbe280d9fac63f63f1b5e43157/CONTRIBUTING.md) and the [CODE_OF_CONDUCT.md](https://github.com/laminas/.github/blob/361a092443d78d33b0f0445bfe4b1ac8e93efc85/CODE_OF_CONDUCT.md) more visible in the components.

At the moment, these files are hidden in the community part (when hitting Insights).

1. Open https://github.com/laminas/.github/
2. Click on "Insights"
3. Click on "Community"
4. Click on either "Contributing" or "Code of Conduct"

Another way of being pointed to these files is under each `textarea` (e.g. when creating/commenting on issues/PRs).
There is a tiny text: `Remember, contributions to this repository should follow its contributing guidelines and code of conduct.`

There are projects which have these files directly stored in all of their components but that is not an option due to the fact that changing these files would need changes in **all** packages.

[Matthew](https://github.com/weierophinney) mentioned, that we could add a `Contributors` section on the website.
[Frank](https://github.com/froschdesign) came up with the idea of linking to these files from within the `README.md`.

Frank will make a suggestion in form of a pull request for the `Contributors` section on the website.

**Questions**:

- Do we want to add links to the `CONTRIBUTORS` and the `CODE_OF_CONDUCT` to the `README.md` of all packages?
- Is there a way of creating **and** merging PRs from CLI for Markdown changes like these?
  There should be no need to release this as a new version of the package so merging this to the default branch would be enough, right?

---

Rob expressed surprise that the contribution information is not in or linked to from the `README.md` file.
Matthew notes that with the transition to Laminas, we started using `.github` repos in each organization, which allows us to keep the guidelines unified across all repositories, but makes discoverability harder.
First-time contributors get a pop-up with the links, but otherwise users must drill-down into the "Insights" section of the repository.

Rob suggests we at least link to the contribution and code of conduct from the `README.md` file of each repo.
Matthew suggests putting these at the bottom of these files, along the lines of:

```markdown
-----

- [Code of Conduct](...)
- [Contributing Guidelines](...)
- [Security Policy](...)
- etc.
```

We agreed this was a no-brainer, and Matthew asked who would like to spearhead this.
He suggests somebody doing a PR on a single repository with proposed text, pinging the TSC to review.
Once approved, we can roll it out more broadly.
[Matthew Setter](https://github.com/settermjd) volunteered to work on the `README.md` changes proposal, and Max indicated he can automate the rollout once the text is approved.

Aleksei noted that the `.github` repo is a kind of technical location, and points out we had a "maintainers" repo under ZF.
He wonders if we should introduce something similar in Laminas.
Matthew notes that this is what the technical-steering-committee repository is for.
Aleksei counters with a question of if we can use it as a documentation source for the website, which led to some confusion by Matthew as this had not been brought up previously in the conversation.
(Aleksei notes it was in the agenda item.)

We agreed that:

- We will update `README.md` files across repositories to add links to contribution documents.
- We will add a build process to the website to grab documents from the `.github` repo and render them.
- We will update the `.github` repo description to mention contribution guidelines, as that repo is pinned in each organization.

### Removal of License File Headers

[Maximilian](https://github.com/boesing) wants to talk about license file headers.
These are outdated as almost all of them are pointing to the `master` branch of the package which does not exist anymore.
As we do have the `LICENSE.md` available in each project, there should be no need to point to it from within every file.
Even tho, having to update the `copyright` header to fit the appropriate "year" is quite annoying.

As Max has plans to integrate source code from non-laminas project (with permission), he can not add the laminas copyright header to that file as the source code was not written by laminas.
So when removing the license headers from laminas-own licenses, we can easily add non-laminas copyright headers (if present - in the example above there are none) to those files which were originally written by 3rd-party.

**Vote for removing license file headers and (if needed) the removal of `malukenho/docheader` check**

---

As it turns out, we voted already to do this in [December 2020](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2020-12-07-TSC-Minutes.md#master-branch-references-and-license-docblocks).
We just need a volunteer to make it happen.
[Geert](https://github.com/GeertEltink) volunteered, and plans on disabling rules around that docblock in the next minor version of our coding standard rules.

### laminas-db Maintainer Vote

Per [#73](https://github.com/laminas/technical-steering-committee/issues/73), we have three laminas-db maintainer
nominations to vote on, and [Matthew](https://github.com/weierophinney) suggests doing it during the meeting to expedite
the vote. As a reminder, the individuals nominated are:

- [Massi Cavicchioli (@MassiCav)](https://github.com/MassiCav)
- [Clark Everetts (@clarkphp)](https://github.com/clarkphp)
- [Slavey Karadzhov (@slaff-at-zend)](https://github.com/slaff-at-zend)

The plan will to be to vote on each individually.

---

We voted on each maintainer, and each was approved uanimously by attending members.

## Next meeting

The next meeting will be held June 7, 2021, at 19:00 UTC.
