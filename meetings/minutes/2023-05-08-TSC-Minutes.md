# Minutes from the 2023-05-08 Laminas Technical Steering Committee Meeting

- When: 2023-05-08 at 19:00 UTC, until 20:23 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Alexei Khudiakov
  - Gary Lockett
  - Michał Bundyra
  - Luís Cobucci
  - George Steel
  - Marco Pivetta
  - Frank Brückner
  - Max Bösing
  - Matthew Setter

Quorum WAS met (9 out of 17 members were present).

## Agenda
### Move settermjd/laminas-static-pages under Laminas

Matthew Setter would like to move his project, [settermjd/laminas-static-pages](https://github.com/settermjd/laminas-static-pages), under the Laminas organisation. To summarise the package:

> It simplifies rendering static pages in Mezzio applications, avoiding the need to create handlers and handler factories to render static content templates.

While he is happy to keep maintaining the package personally, he thought that it would be a good addition to the Laminas project.

#### Discussion

A few questions arose as to the purpose and whether it would sit alongside our other template implementations for mezzio. Matthew clarified that it would, at which point the topic of
maintenance responsibility was mentioned. It was agreed that Matthew would be the primary maintainer of this repository and members expressed their support for inclusion.

A poll was created leading to a unanimous vote in favour of including the component in the Laminas organisation.

### Fork mezzio/mezzio-swoole as mezzio/mezzio-openswoole

Openswoole starting with version 22.0 began diverging from swoole with new unique functionality, existing api deprecated and some previously deprecated api removed. See 
https://openswoole.com/article/v22-0-0-released#changelog For example, method `swoole_set_process_name()` was replaced with `OpenSwoole\Util::setProcessName()`, see 
https://github.com/mezzio/mezzio-swoole/issues/110

Alexei Khudiakov proposes that we create a fork to somewhat eleviate the maintenance burden.

> It is evident that supporting both extensions within same component will be increasingly difficult and potentially stiffing for addition of a new functionality.

Alexei proposes that we:
- Fork mezzio/mezzio-swoole as mezzio/mezzio-openswoole.
- Declare explicit dependency on respective extensions with version ranges
- Improve CI for those two components to run unit and integration tests in matrix with every supported extension version. At minimum with each major and ideally with each minor as well.

#### Discussion

The initial reactions of members was that we should stick to a single implementation and that it would be better to choose between Swoole and OpenSwoole rather than maintaining an
implementation for both.

Gary raised a concern wether a `mezzio-async` common package would be necessary. Alexei noted however, that `mezzio-swoole` doesn't offer any async support by itself and merely bridges the
gap between `mezzio` and `swoole`, meaning there is not much if anything that would be reusable.,

Marco requested further insight into a) the reason for the fork, whether an RCE risk was still a possibility and b) as to what the usage statistics of swoole vs openswoole were. The popularity
of both of these packages was highlighted and several versions of figures trended towards swoole being the most used of the two.

The decision to drop one extension, fork the component, or choose one over the other was debated and no concensus was reached with a vote resulting in 5 abstains. It was suggested to discuss
the topic further at the next meeting for potential input from other TSC members.
