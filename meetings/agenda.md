# Next Technical Steering Committee Meeting Agenda

- Date: 2020-09-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

- PHP 8.0 introduction in packages

  As we are about to support PHP 8.0, what is our strategy to do so?
  - Do we want to support PHP `8.0` or `8.*`? (`php: ^8.0` *vs* `php: ~8.0.0`)
  - How can we provide PHP 8 support in *every* package? 
  
    There are several ways of ignoring platform reqs (which is necessary in some cases due to the fact that some packages are not yet compatible). 
    
    Do we have best-practice examples on how to work on supporting PHP 8? Ignoring `platform-reqs` is just one side of the coin. Do we contribute to upstream libraries in case these are blockers to migrate a laminas package?

  - Should we open PHP 8 organization projects to public and create a script to create issues on every project which is not yet PHP 8 compatible?
  
  - Do we want to create a HOWTO where we provide expectations on how a PR might look like?
    - `composer.json` has a constraint for PHP 8.0 and might drop [PHP versions which are unsupported](https://php.net/supported-versions)?
    - `composer.json` contains phpunit version which can run with PHP 8.0
    - `.travis.yml` contains php nightly in matrix (with or without allow-failures?)
    - *anything else?*
