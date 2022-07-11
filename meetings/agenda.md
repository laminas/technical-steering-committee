# Next Technical Steering Committee Meeting Agenda

- Date: 2022-07-11
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Future of the migration layer

We should think about how to proceed with `laminas/laminas-dependency-plugin` and `laminas/laminas-zendframework-bridge`.
Due to the latest issues reported in the zendframework bridge (https://github.com/laminas/laminas-zendframework-bridge/issues/95 https://github.com/laminas/laminas-zendframework-bridge/pull/94) and the recent movement of composer not following semver anymore, archiving both `laminas/laminas-dependency-plugin` with `laminas/laminas-zendframework-bridge` might be considered as the best option.

Abandoning old migration stuff after 2,5 years might be okay.

So questions are: 
 - Should we abandon both packages? 
 - What components do still rely on the bridge?
 - Should we release a new version of these components relying on the bridge so they're not blocking upstream projects getting rid of the bridge?

### Possibilities for project backers

In the early TSC-meetings the funding of the project as well as possibilities for backers were discussed. A thing I remember, but cannot find in the minutes, was some idea project backers to be listed in some form on the website. Maybe it was in connection with a list of "official" agencies providing support.

The topic has not been discussed recently. I would like to know if there are any news on this? 

### Composer v2

Composer [v2.0.0](https://github.com/composer/composer/releases/tag/2.0.0) was released on end of October 2020.
Since then, the usage of `ocramius/package-versions` became obsolete and therefore, `composer/package-versions-deprecated` was already used to "override" `ocramius/package-versions`.

Due to Marcos amazing idea of providing runtime information for composer dependencies, composer added this as a native feature with v2.0.0.

However, we do still depend on the `composer/package-versions-deprecated` dependency as it does support PHP 8.0 and PHP 8.1 in the v1.x range while `ocramius/package-versions` would also require the v2+ version of it.
In components which do support PHP 7.4 + PHP 8.0, we are forced to use the composer replacement.

We do have two options as of november this year:

1. remove PHP 7.4 support, remove `composer/package-versions-deprecated` and re-add `ocramius/package-versions` since it supports PHP 8.0 as of v2
2. remove `composer/package-versions-deprecated` and require `composer-runtime-api` v2. This will ensure, that we can use `\Composer\InstalledVersions` without the need of any 3rd-party component.

**Question is:** Do we want to start requiring composer v2 in our components when it comes to features like `\Composer\InstalledVersions` or should we still allow composer v1 even if we started to drop composer v1 in our composer plugins?
