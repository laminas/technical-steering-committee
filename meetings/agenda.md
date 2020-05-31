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

- Laminas/Mezzio Release Cycle
  
  I would like to talk about what release cycles we might want to achieve.
  
  These are the release cycles of other frameworks:
  
  #### symfony
  Time-based release cycle every 6 months (May/November).
  
  #### Yii
  Extension releases (not quite sure what that is tbh) are tagged on a weekly-base.
  Framework itself is tagged once a month.
  
  #### Drupal
  Release windows depending on release.
  Key dates are on a monthly base.
  
  - First wednesday of every month for bugfix releases
  - Third wednesday of every month for security releases
  
  There are merge windows for new releases.
  
  #### Laminas/Mezzio
  
  I did not research every repository. However, in the laminas-http repository, which is required by the most-installed laminas-mvc package, there are a few bugfixes pending since january/february 2020.
  
  For example:
  - [laminas/laminas-http#31](https://github.com/laminas/laminas-http/pull/31)
  - [laminas/laminas-http#34](https://github.com/laminas/laminas-http/pull/34)
  
  I accidentally opened up a bugfix which was already patched back in february but not released end of may.
  
  Therefore, treat this as a RFC for a laminas release cycle which allows users to have their own contributed fixes in a frustration-free timeframe. If we have fixed release cycles for minors/bugfixes, I think its easier to take time to focus on those releases instead of doing this besides other stuff.
  
  I kinda like the release cycle of drupal which includes fixed dates so one can focus on releasing maintained packages. I see the problem that one might be not available at that time (e.g. holidays, ...) but there ain't new versions for every package every month *and* there might be always someone of the TSC who probably can step in for that special case.
  
  I am not that familiar with release cycles and thus like to hear what the others have to say about this. 
