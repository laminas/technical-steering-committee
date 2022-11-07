# Minutes from the 2022-11-07 Laminas Technical Steering Committee Meeting

- When: 2022-11-07 at 19:00 UTC, until 19:31 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brückner
  - Gary Lockett
  - George Steel
  - Luís Cobucci (arrived 32 minutes in, just after discussion was complete :smiley:)
  - Marco Pivetta
  - Maximilian Bösing
  - Matthew Setter (at 44 minutes in, after official discussion had ended)
  - Matthew Weier O'Phinney
  - Michał Bundyra
  - Rob Allen

Quorum WAS met (12 out of 15 members were present).

We met for around a half-hour, and then opened the floor to additional discussion.
Since that discussion was not part of the agenda, I have left it off the minutes.

## Agenda

### RFC - Deprecate `laminas-filter` compression adapters: `rar`, `lzf`, `snappy`

@gsteel proposes that these adapters are deprecated in the next minor for removal in the next major. The primary reason for deprecation is maintenance burden - none of the extensions are available as OS packages and must be compiled or installed via pecl.

[RFC Link](https://github.com/laminas/laminas-filter/issues/79), Further discussion in [PR #78](https://github.com/laminas/laminas-filter/pull/78)
#### Discussion

The main reason to deprecate these filters is due to their reliance on optional extensions, which makes testing against them exponentially more difficult (particularly when they cannot be installed even using standard tooling like PECL).
The next question raised is if these formats are even widely used, and the consensus was most of us have never encountered them in the wild when developing web applications.

#### Decision

We took a vote of the 10 members present at the time. 8 voted in favor of the RFC, with 2 abstaining.

### Magento PHP 8.2 support

Adobe has inquired as to whether or not we can address PHP 8.2 support on the following:

- laminas-captcha
- laminas-code
- laminas-db
- laminas-di
- laminas-file
- laminas-oauth
- laminas-soap

Of these, laminas-db, laminas-file, laminas-oauth, and laminas-soap are all packages we've marked feature-complete, and laminas-code support for 8.1 is still on-going. Additionally, many have dependencies on other packages, which means that the list is likely at least 2x longer. Are we interested in entertaining these requests?

Matthew noted that last year we requested of them that they submit PRs, and encouraged a financial donation; neither happened.
Instead, we had a team of volunteers doing unpaid work for a commercial entity.
He does not feel comfortable committing contributors and maintainers to that.

The consensus was that Matthew will write back to them, expanding the list of packages to detail the dependency packages also involved, how to contribute (including updates to `.laminas-ci.json` as needed), and that we will not review PRs where the CI/CD is not passing.
