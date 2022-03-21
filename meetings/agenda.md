# Next Technical Steering Committee Meeting Agenda

- Date: 2022-04-04
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss


### `laminas-view` v3.0 RFC

[Gary Lockett](https://github.com/internalsystemerror) filed an RFC for consideration in `laminas-view` [#149](https://github.com/laminas/laminas-view/issues/149) for an overall simplification of `laminas-view` that would include significant BC breaks for a number of related projects, possibly requiring new majors in those components too, for example `laminas-form` and `i18n`.
  By way of example, he opened [laminas/laminas-i18n#75](https://github.com/laminas/laminas-i18n/pull/75) that provides incremental changes to move towards compatibility with a 3.0 release of view.
  The overall goal of this 'simplification' is to make laminas-view as stateless as possible and appropriate for use outside of MVC: on the CLI, rendering email message views, running under Open/Swoole/React/Whatever without hidden state gotchas.

### Composer v1 support

[Maximilian Bösing](https://github.com/boesing) wants to get a decision on how to proceed with laminas/mezzio composer plugins and support for composer v1. As of https://github.com/laminas/laminas-component-installer/pull/46, composer v1 tests are executed for PHP 8.1 (wasn't the case prior this patch) and the tests were failing due to some incompatibility of composer v1 and phpunit reporting deprecations as exceptions. [Marco Pivetta](https://github.com/Ocramius) suggested to drop support for composer v1 entirely to get rid of the failing v1 tests.

To get a final decision here (as composer v1 received a release in january this year), we should talk about this in the TSC meeting.

### `laminas-servicemanager` container-interop further actions

[Maximilian Bösing](https://github.com/boesing) wants to talk about the further actions regarding the `container-interop` problematic in `laminas-servicemanager`.
In [laminas/laminas-servicemanager#96](https://github.com/laminas/laminas-servicemanager/pull/96), he created a proof of concept implementation of how to `replace` container-interop from within the `laminas-servicemanager` component directly. 
After creating that PoC, Max created a [Pull Request](https://github.com/php-fig/container/pull/38) in `psr/container` to let that package `replace` the `container-interop` package. Due to some politics and to the whole FIG process, discussions led to create a [Pull Request](https://github.com/container-interop/container-interop/pull/97) in `container-interop` implementation instead.
After some reviews, some drawbacks were that projects which do provide their own container might implement both `PSR-11` and the working group interface from `container-interop`. When dangling with `class_alias`, this will lead to duplicated interface implementation issues:

1. Working code example of code implementing both interfaces: https://3v4l.org/cemXs#v8.1.4
2. Broken code example of code implementing both interfaces after juggling with `class_alias`: https://3v4l.org/Zh1OR#v8.1.4

So even if we add `replace` to `laminas-servicemanager`, this will lead to issues in upstream projects. That's (and a [blog post comment](https://blog.naderman.de/2014/02/17/replace-conflict-forks-explained/#comment-5) from [Matthew](https://github.com/weierophinney) in 2014) led Max to think about another solution which is based on the dependency inversion principle. We added dependency inversion to `laminas-cache` starting with [v3.0](https://github.com/laminas/laminas-cache/blob/86b47eb7b05bc4d24edafb3039494ba81405983b/composer.json#L32) to require upstream projects to require at least one specific cache implementation.

The `laminas-servicemanager` component could require such a package in a new minor version as well while dropping it again in the next major. This approach has several benefits towards just `replace` the `container-interop` package:

Upstream projects...

- can run `composer update` without actually getting uninstalled `container-interop` without their permission
- can migrate all their own factories to consume `PSR-11` container interface
- can verify their own 3rd-party deps to verify if one of these are still consuming interop `ContainerInterface`
- can change own `ContainerInterface` implementations to remove the interop interface usage

If everything is fine, the project can add the implementation we do require with `laminas-servicemanager` as part of their `composer.json` like this:
```json
{
  "...": {},
  "provide": {
    "laminas/container-interop-replacement-implementation": "1.0.0"
  }
}
```

This would not include any new dependency and the next `composer update` will properly bump `laminas-servicemanager` to a version without `container-interop`.

This will also provide a way to migrate our own implementations and 3rd-party dependencies afterwards. Implementations from laminas of the `laminas-servicemanager` `AbstractPluginManager` are:

- [laminas-mvc](https://github.com/laminas/laminas-mvc/blob/ae0dbea9aed39dd6cb85f998b5ca4df320df90fd/src/Controller/ControllerManager.php#L18)
- [laminas-mvc](https://github.com/laminas/laminas-mvc/blob/ae0dbea9aed39dd6cb85f998b5ca4df320df90fd/src/Controller/PluginManager.php#L16)
- [laminas-view](https://github.com/laminas/laminas-view/blob/6e623ccabfcd26999ce836990e5157125b58aede/src/HelperPluginManager.php#L35)
- [laminas-validator](https://github.com/laminas/laminas-validator/blob/bdd503adc83d814a5c94e598ea0eb9fc7ca56339/src/ValidatorPluginManager.php#L49)
- [laminas-cache](https://github.com/laminas/laminas-cache/blob/1a6e688271793a0e3cd7eb43aec063526c931047/src/Storage/AdapterPluginManager.php#L14)
- [laminas-cache](https://github.com/laminas/laminas-cache/blob/1a6e688271793a0e3cd7eb43aec063526c931047/src/Storage/PluginManager.php#L17)
- [laminas-filter](https://github.com/laminas/laminas-filter/blob/88ed9340e0bd099ac9f5a06244ddd6e660196161/src/FilterPluginManager.php#L29)
- [laminas-hydrator](https://github.com/laminas/laminas-hydrator/blob/bb206b06377092982987a018d34243579eed5482/src/HydratorPluginManager.php#L21)
- [laminas-serializer](https://github.com/laminas/laminas-serializer/blob/f5d9e0e0f56bc92acdfd7a2aa8212940d6edbcee/src/AdapterPluginManager.php#L28)
- [laminas-inputfilter](https://github.com/laminas/laminas-inputfilter/blob/5d8986654c8b455192cd180985634f9eacf56501/src/InputFilterPluginManager.php#L23)

Most of these plugin managers do not provide factories but might still be used by upstream projects which do use factories using the interop interface.

In case, an upstream project is not 100% sure if everything is properly migrated within their own dependency tree, a (not yet created) laminas component could be required which does the actual `class_alias` magic. However, this has to be explicitly required by an upstream project and therefore gives these projects 100% control of how to proceed.

Examples of both project starting points were made in the proof of concept pull request [laminas/laminas-servicemanager#96](https://github.com/laminas/laminas-servicemanager/pull/96).

The TSC should talk about both proof of concepts and make a decision on how to proceed:

a) Use `replace` in `laminas-servicemanager` to quickly get rid of `container-interop` (does not require changes in other components but might have drawbacks due to the `replace` usage)
b) Use the `dependency inversion` approach which requires upstream projects to decide whether to `replace` or to handle the `container-interop` issue by themselves (requires work on other components)
