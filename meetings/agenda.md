# Next Technical Steering Committee Meeting Agenda

- Date: 2022-11-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### RFC - Deprecate `laminas-filter` compression adapters: `rar`, `lzf`, `snappy`

@gsteel proposes that these adapters are deprecated in the next minor for removal in the next major. The primary reason for deprecation is maintenance burden - none of the extensions are available as OS packages and must be compiled or installed via pecl.

[RFC Link](https://github.com/laminas/laminas-filter/issues/79), Further discussion in [PR #78](https://github.com/laminas/laminas-filter/pull/78)

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
