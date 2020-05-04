# Next Technical Steering Committee Meeting Agenda

- Date: 2020-06-01
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

- mezzio-cors library

  Max [@boesing](https://github.com/boesing) created an [Expressive module](https://github.com/boesing/zend-expressive-cors)
  which can be used to provide proper CORS details to browsers.
  
  In 2017, he contributed to the MVC module
  [zfr/zfr-cors](https://github.com/zf-fr/zfr-cors/pull/43) to provide per-route
  configuration for CORS. As there is no such library which allows project and
  per-route configuration for CORS in mezzio applications, we might want to move
  it to the mezzio organization.

  **Questions in case we move it to the mezzio organization**

  - The library uses `options.defaults` in route configuration. Should we change
    it to `options` instead to keep request attributes clean?

- Mezzio Project - Update

  Create new project to track progress with mezzio components.  Set the fixed
  date: 1st of Dec, 2020 (PHP 7.2 has security only support until 30th of Nov,
  2020).

  Update all mezzio components:
  - drop support for PHP prior to 7.3
  - add PHP 7.4 build with lowest and latest dependencies
  - add phpstan or psalm
  - update all dependencies to latest version and drop previous versions
  - solve PHPUnit warnings in tests (support only PHPUnit ^9.1)
  - update to LCS v2 (need to be released before)
  - review all open issues and PRs, reply, close or address with new minor/bugfix
  - report tickets for new major (if there is deprecated functionality which
    should be removed etc)
  - rewrite existing commands to use laminas-cli (keep current commands and mark
    them deprecated)
  - write new commands or at least reports tickets what commands we should add
    in each component and link to laminas-cli project

  Order of update does matter, so we can pin latest versions in skeleton/mezzio.

  - Do we want to do this?
  - Can we achieve it?
  - Any other suggestions?

- Vote on new members:
  - [Matthew Setter (@settermjd)](https://github.com/settermjd) (nominated by @Xerkus)
