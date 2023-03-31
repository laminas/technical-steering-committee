# Minutes from the 2023-03-06 Laminas Technical Steering Committee Meeting

- When: 2023-03-06 at 19:00 UTC, until 20:21 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan (arrived 19:44 UTC)
  - Alexei Khudiakov
  - Frank Brückner
  - Gary Lockett
  - George Steel
  - Luís Cobucci
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra
  - Rob Allen

Quorum WAS met (10 out of 15 members were present).

## Agenda

### `ServiceManager` return type synchronization with `ContainerInterface` 

We do have plenty of places where `FactoryInterface`, `ServiceManager#doCreate` (which is consumed by `ServiceManager#get`) and some other interfaces which state that an object is being returned.

The `PSR-11` `ContainerInterface#get` method explicitly states to return `mixed` as a container can return *everything*.
That's also the case when we look into the Laminas world.
Even though we do state it returns `object`, *every* factory can actually return arrays, scalars, and whatever else might be returned.
Due to the lack of native return types, there is no validation happening and thus in upstream projects might exist plenty of factories returning whatever values.

The initial change to expect `object` was made in https://github.com/laminas/laminas-servicemanager/commit/1cd5bedf83c3d93f797a9224964595155703d56d.
It seems that these changes were made after some code-review feedback in https://github.com/laminas/laminas-servicemanager/pull/98#discussion_r709268923.

However, as we already know, when using `ContainerInterface#get` with i.e. the value `config`, we may retrieve an array (the merged application config) rather than an object.
In https://github.com/laminas/laminas-servicemanager/pull/179, `mixed` was allowed to be returned from all factories for now so that it reflects the actual return types from `ContainerInterface`.

This item is brought to the TSC meeting to outline if we want to:

- allow `mixed` in the future to be returned from all factories (thats esp. helpful when it comes to the nullable `instanceOf` inheritance type in `AbstractPluginManager`)
- want to enforce `array|object` as the return type of `ServiceManager#get` which might have impact on upstream projects returning whatever value from their factories

As a sidenote, Symfony` did limit the return values of their `ContainerInterface` to `null|object`.
If we want to go down that route as well, we need to find a way on how to proceed with the merged application config.

#### Discussion

Matthew asked what rationale Symfony used for restricting their container to objects or `null`, and noted that removal of `array` return values would be a BC break in Laminas and Mezzio due to our `config` service.
He also noted that allowing return of `null` by Symfony feels like a way to bypass a `has()` check (e.g. to use with the null safe operator, `$container->get($serviceName)?->someOperation(...)`).
Nobody was certain what Symfony's motivations were, and Marco pointed out that the spec indicates that failure to resolve a service in `get()` should properly throw an exception, not return `null`.

Marco asked if expanding our typehint to `: mixed` would lead to a BC break.
Aleksei felt it was okay for us to limit to object and array, but others pointed out that the PSR-11 spec actually says `mixed` for the return type, so limiting it artificially feels like breaking with the spec.
(Specific examples brought up were the return of `resource` instances, many of which are still not objects, and returning application secrets, which will typically be scalars.)

Marco clarified his position: why are we discussing this at all?
Max pointed to the `AbstractPluginManager`, where it might make sense to restrict to a specific type or union.
Since reducing what is returned follows LSP rules, nobody had a problem with this.

There was some continued discussion about whether or not a registered service was allowed to return `null`, or if this would be indicative of "no service".
Matthew pointed out that `null` should be fine:

- A service may be defined only in specific environments (e.g., a debug service you do not want available in production); usage of the null safe operator allows it to be consumed safely.
- Misconfiguration means `null` is returned, but consumers want non-null, in which case you get a type error.
  Since this latter condition typically happens during instantiation of a class, it will generally happen in a factory and be close to the consumer anyways.

Max noted that the effort to restrict to specific types is bigger than allowing everything.
Matthew followed by indicating this would be BOTH a BC break with our existing code base, AND a break with the PSR-11 spec.
It's easiest to keep our usage as documented and specified, except in the case of plugin managers, where it makes sense to indicate the specific types or unions.

#### Decisions

We held a vote, and decided to add an explicit `mixed` return type for the laminas-servicemanager `ServiceManager` implementation.

### Unification of efforts in developing an API application based on Mezzio

DotKernel are actively developing, maintaining and using in production a simple REST API project , built around Mezzio API skeleton proposed by @ezimuel 5 years ago. 

The repository is here : https://github.com/dotkernel/api

What if we join the efforts,  Laminas and Dotkernel, to have only one production-ready REST API , and build from there a replacement of laminas-api-tools.

I am ready to move the repository under Mezzio organisation, and provide part time developers to handle the future development. 

#### Discussion

Julian Somesan, from dotKernel and Apidemia (a Laminas Commercial Vendor), joined the discussion.
He provided some more details on dotKernel:

- It provides Doctrine integration
- It provides Twig integration
- It provides lamians-email + Twig integration for sending emails
- It integrates with Postman
- It provides an error collector
- They provide an Angular starter kit for dotKernel APIs.

Essentially, a lot of what Apigility/Laminas API Tools have provided, but for Mezzio.
They have explicitly not created the admin GUI present in those projects, to encourage developers to learn how it works under the hood.
(Matthew noted that this was the biggest time sink when developing the original project, and it's unlikely Laminas will ever have enough people to dedicate to something like that again.)

Rob then asked what the benefit is to Apidemia to having Laminas adopt dotKernel.
Julian replied simply "portfolio".

Marco noted that Apidemia has more development resources to throw at the project than Laminas, and is best positioned to maintain it and steer direction.
Matthew noted that perhaps it might make more sense for Laminas to _recommend_ dotKernel for those wanting to develop APIs with Mezzio.
This would give the visibility they are looking for, without adding additional maintenance burden to Laminas.
If some components would be generally useful in Mezzio, they could be proposed individually, but otherwise stay under the dotKernel umbrella.
Julian agreed with this plan.
Laminas TSC members will do some more investigation of the dotKernel project to ensure everyone is comfortable with recommending it to users, and then we can work on cross-promotion.

Additionally, we discussed adding the dotKernel developers as maintainers on Mezzio packages.
We indicated that this would definitely be welcome, as more maintainers is never a bad thing.
However, as usual, we need to see a history of pull requests and interaction with the project before adding anyone.
Julian promised to open a PR to the TSC repo to discuss maintainer roles for next meeting.
