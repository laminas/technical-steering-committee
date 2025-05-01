# Next Technical Steering Committee Meeting Agenda

- Date: 2025-05-05
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Release version 3.0 of `laminas-filter`

@gsteel proposes to release v3 of `laminas-filter`: [V3 Milestone](https://github.com/laminas/laminas-filter/milestone/4?closed=1)

#### Primary Changes

- Service Manager v4 Support
- All filters refactored to:
  - Remove inheritance entirely (No more abstract filter)
  - All filters are now final
  - Consistently accept options, as an array in the constructor
  - Remove all runtime mutation
  - Parameter and return types throughout

The [migration guide](https://github.com/laminas/laminas-filter/blob/3.0.x/docs/book/v3/migration/v2-to-v3.md) is complete and serves as a good overview of all the changes

### Release version 1.0 of `laminas-navigation-view`

@gsteel proposes to release v1 of [`laminas-navigation-view`](https://github.com/laminas/laminas-navigation-view)

This is a new package that contains view helpers related to `laminas-navigation`. In order for `laminas-view` to reach a v3 release, a number of dependencies need to be de-coupled so that view can be upgraded to support service manager v4.

V1 is a straight copy of the files in `laminas-view` except the namespace change and marking classes as final where possible.

The plan is to work on and release a v2, _after_ `laminas-view@3.0` has been released which will make the necessary changes for `laminas-navigation-view` to support `service-manager@4.x` and `laminas-view@3.x`

It is likely we'll need to do something similar for `laminas-paginator`…

### General Discussion on Soft-Dependency Satellite Packages

I currently have the problem of a `laminas-paginator` soft-dependency in [`laminas-view`#279](https://github.com/laminas/laminas-view/issues/279)

Can we reach a consensus on how to refactor packages to remove soft-dependencies, or, at least resolve the issues specifically for `laminas-view` which are now limited to:

- `laminas-filter` (Which I would like to drop, and replace with a generic callable for view filtering)
- `laminas-authentication` Where should the `Identity` view helper go? To the auth package? a separate pkg?, or keep the soft dep?
- `laminas-paginator` Same question… Keep the soft dep and require SMv4 support in paginator first, move to a new pkg, move to paginator (thereby introducing a dependency on view)

If we decide that satellite packages should be created, then we should probably have a vote on creating new packages for

- `laminas-paginator-view`
- `laminas-authentication-view`

Generally, cyclic _soft_ dependencies are everywhere, traversing to `laminas-authentication` from here brings up soft-deps on `validator` amongst several others.

### The Future of MVC

Modernising, refactoring and adding support for service manager v4 in the various libs is a lot of work.
Affordances for the MVC framework take additional effort.
Given the lack of maintenance activity on the MVC side of things, is it time to consider the long-term future of MVC?
