# Next Technical Steering Committee Meeting Agenda

- Date: 2023-03-06
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### `ServiceManager` return type synchronization with `ContainerInterface` 

We do have plenty of places where `FactoryInterface`, `ServiceManager#doCreate` (which is consumed by `ServiceManager#get`) and some other interfaces which state that an object is being returned.

The `PSR-11` `ContainerInterface#get` method explicitly states to return `mixed` as a container can return *everything*. Thats also the case when we look into the laminas world. Even tho, we do state it returns `object`, *every* factory can actually return arrays, scalars and whatever else might be returned.
Due to the lack of native return types, there is no validation happening and thus in upstream projects might exist plenty of factories returning whatever values.

The initial change to expect `object` was made in https://github.com/laminas/laminas-servicemanager/commit/1cd5bedf83c3d93f797a9224964595155703d56d. It seems that these changes were made after some code-review feedback in https://github.com/laminas/laminas-servicemanager/pull/98#discussion_r709268923.

However, as we already know, when using `ContainerInterface#get` with i.e. the value `config`, we may retrieve an array (the merged application config) rather than an object. In https://github.com/laminas/laminas-servicemanager/pull/179, `mixed` was allowed to be returned from all factories for now so that it reflects the actual return types from `ContainerInterface`.

This item is brought to the TSC meeting to outline if we want to:
- allow `mixed` in the future to be returned from all factories (thats esp. helpful when it comes to the nullable `instanceOf` inheritance type in `AbstractPluginManager`)
- want to enforce `array|object` as the return type of `ServiceManager#get` which might have impact on upstream projects returning whatever value from their factories
