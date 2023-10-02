# Minutes from the 2023-08-07 Laminas Technical Steering Committee Meeting

- When: 2023-08-07 at 19:00 UTC, until 19:46 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Alexei Khudiakov
    - Andreas Heigl
    - Gary Lockett
    - Luís Cobucci
    - Marco Pivetta
    - Matthew Weier O'Phinney
    - Max Bösing
    - Michał Bundyra
    - Rob Allen

Quorum WAS met (9 out of 15 members were present).

## Agenda

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

#### Discussion

The initial discussion was clarification of the functionality and why it exists.
The point is allowing serialization of any PSR-7 message primarily to string, and secondarily to an array structure.
On the flip side is deserialization of a string HTTP message or array structure to a PSR-7 message using a PSR-17 factory.
The current implementation in Diactoros only allows deserialization using Diactoros messages.

Marco understood the string de/serialization, but feels that the array variant likely is something better suited for a log handler or other implementation, as there is no standard structure to use.
Keeping it creates more complexity.

Luís asked if it should be parsing the request body based on the content-type header, or if it should provide abstractions around that.
Matthew noted that there's no parsing that needs to be involved, other than any work needed to select the appropriate stream implementation, which would be the responsibility of the PSR-17 factories.

Finally, Marco pointed out that even if we are providing a single implementation, and that that implementation is really the only one needed to follow the spec, we should still provide interfaces, to allow alternate implementations that need to do customization (e.g., treatment of multi-line headers, multi-part content, etc.).

#### Decision

Matthew will:

- Remove array de/serialization
- Add interfaces for each direction of each message type (e.g. `ResponseToString`, `StringToRequest`, etc.)
- Deprecate array de/serialization in Diactoros, indicating it will be removed
- Deprecate string de/serialization in Diactoros, indicating it will be removed, but that users can move to the new package immediately for this functionality
- The _implementation_ of the interfaces may be done in a single class, implementing both interfaces; this detail is still TBD.

Additionally, he will do another iteration on the new package and bring it back to the TSC for review when ready.

### laminas-api-tools and Renovate

Now that Matthew W has completed work on updating laminas-api-tools to PHP 8.2, he is curious if we should add Renovate to that organization to assist with updating to new PHP versions.
Since we decided to no longer _actively_ support these components, this would at least allow users to (potentially) use them with newer PHP versions as they are released.

#### Discussion

The initial discussion was clarifying that Matthew W had completed the work to get laminas-api-tools tested against PHP 8.2, _including_ getting Psalm added and laminas-coding-standard updated to the latest versions.

Once that was clarified, he proposed that we just go ahead and add Renovate and see what happens when 8.3 drops.
If it's too painful, we disable it and point to the "no longer maintained" announcements; if it's not, we get things updated.

This was deemed acceptable, and then the question turned to how to enable Renovate on these repos, and if we can keep the number of scans by Renovate down to an acceptable minimum (such as weekly, monthly or quarterly).
