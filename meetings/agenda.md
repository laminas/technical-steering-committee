# Next Technical Steering Committee Meeting Agenda

- Date: 2023-05-08
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

### Move settermjd/laminas-static-pages under Laminas

Matthew Setter would like to move his project, [settermjd/laminas-static-pages](https://github.com/settermjd/laminas-static-pages), under the Laminas organisation. To summarise the package:

> It simplifies rendering static pages in Mezzio applications, avoiding the need to create handlers and handler factories to render static content templates. 

While he is happy to keep maintaining the package personally, he thought that it would be a good addition to the Laminas project. 

### Fork mezzio/mezzio-swoole as mezzio/mezzio-openswoole

Openswoole starting with version 22.0 began diverging from swoole with new unique functionality, existing api deprecated and some previously deprecated api removed. See https://openswoole.com/article/v22-0-0-released#changelog
For example, method `swoole_set_process_name()` was replaced with `OpenSwoole\Util::setProcessName()`, see https://github.com/mezzio/mezzio-swoole/issues/110

It is evident that supporting both extensions within same component will be increasingly difficult and potentially stiffing for addition of a new functionality.

I propose we:
- Fork mezzio/mezzio-swoole as mezzio/mezzio-openswoole.
- Declare explicit dependency on respective extensions with version ranges
- Improve CI for those two components to run unit and integration tests in matrix with every supported extension version. At minimum with each major and ideally with each minor as well.
