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
