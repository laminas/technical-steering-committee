# Next Technical Steering Committee Meeting Agenda

- Date: 2020-05-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

- mezzio-cors library

  max [@boesing](https://github.com/boesing) created an [expressive module](https://github.com/boesing/zend-expressive-cors) which can be used to provide proper CORS details to browsers.
  
  In 2017, he contributed to the MVC module [zfr/zfr-cors](https://github.com/zf-fr/zfr-cors/pull/43) to provide per-route configuration for CORS. As there is no such library which allows project and per-route configuration for CORS in mezzio applications, we might want to move it to the mezzio organization.

  **Questions in case we move it to the mezzio organization**
  - The library uses `options.defaults` in route configuration. Should we change it to `options` instead to keep request attributes clean?
