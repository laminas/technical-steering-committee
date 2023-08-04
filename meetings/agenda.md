# Next Technical Steering Committee Meeting Agenda

- Date: 2023-08-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### laminas-psr7-serializer

We've had an [open request to separate our PSR-7 serializers into a separate package](https://github.com/laminas/laminas-diactoros/issues/43) for several years now.
During the updates of Diactoros to PSR-7 v2, it came up again, and Aleksei originally suggested we do that during that update.
Matthew pushed back because it was a larger effort, involving:

- Creating a new package for the serializers
- Doing a minor version of Diactoros to (a) deprecate its implementations, and (b) update them to proxy to the classes exposed in the new package
- Doing a new major of Diactoros to remove the existing serializers, and instead recommend the new package

At this time, Matthew W has completed work on the [new serialization package](https://github.com/weierophinney/laminas-psr7-serializer), and proposes:

- Bringing it into the main Laminas organization
- Performing the second step, above, of doing a new Diactoros minor with deprecations/proxies

### laminas-api-tools and Renovate

Now that Matthew W has completed work on updating laminas-api-tools to PHP 8.2, he is curious if we should add Renovate to that organization to assist with updating to new PHP versions.
Since we decided to no longer _actively_ support these components, this would at least allow users to (potentially) use them with newer PHP versions as they are released.
