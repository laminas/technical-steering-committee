# Minutes from the 2021-02-01 Laminas Technical Steering Committee Meeting

- When: 2021-02-01 at 19:00 UTC, until 20:00 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Frank Brückner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra

Quorum was met (8 out of 15 members were present).

## Agenda

- [Artem Zakirullin](https://github.com/zakirullin) has requested we discuss and vote on his [proposed laminas-service-inspector package](https://github.com/laminas/technical-steering-committee/issues/55).

## Updates

[Matthew](https://github.com/weierophinney) provided a quick update of progress on initiatives since the previous month:

- [Marco](https://github.com/Ocramius), [Cees-Jan](https://github.com/WyriHaximus), and Matthew met the same week as last month's TSC meeting and hammered out requirements for the GitHub Actions CI pipeline.
  We've got a stable version up and running that we've been iterating on, and the instructions for adding it are here: https://gist.github.com/weierophinney/9decd19f76b7d9745c6559074053fa65

- Matthew added the GHA CI pipeline to all repositories we chose to mark as security-only, issued releases that support PHP 8.0, and marked those repos security-only at this time, with the exception of the laminas-mail repo (which now has a maintainer!).

- We could use some help getting the pipeline rolled out to other repositories. :smile:

## Laminas Service Inspector

Initial discussion of the proposed service manager inspector was around whether it should be a standalone utility, or a [Psalm](https://psalm.dev) plugin.
Marco suggested it be a Psalm plugin, as this wuold allow re-use of existing Psalm inferred types.
He and [Max](https://github.com/boesing) also suggested that all classes it creates be marked final and internal, to allow continuous refactoring, as Psalm moves so quickly, and we will need to be free to rewrite without worrying about API breakage.

Marco suggested that one other reason for using Psalm is that the tool will then be able to use the AST, which will make it both performant, and more accurate.
However, Max noted that for the tool to be useful, it needs to know what the final container configuration is, which generally requires parsing the `config/config.php` file in Mezzio applications and the `config/application.config.php` file in MVC applications.
On top of that, because configuration varies based whether or not you are in development mode, or which "local" configuration files are present, the ability to have a run-time check can be incredibly useful.
In point of fact, many types can only be resolved once all configuration merging is complete as the order of configuration files will dictate it.
But this makes having it operate only on the AST next-to-impossible.
On top of that, [Geert](https://github.com/geerteltink) noted that limiting it to a Psalm plugin would mean making it inaccessible to people using other static analysis tools, or those who are not familiar with Psalm and do not need it for anything else.
Marco conceded that his only real concern is that the tool be "as-static-as-possible"; one of his use cases for such a tool is to help him analyze codebases to understand how various services are constructed, and what they depend upon.

At this point, Matthew summarized the consensus:

- Ship it as a standalone binary
- potentially as part of laminas-servicemanager, but potentially in its own repo
- with an eventual goal of running fully statically (no runtime),
- but using runtime code is fine for now.

Matthew asked Marco for clarification of the verbiage "standalone binary", asking if a laminas-cli command would work, or if he was wanting a completely separate binary.
Marco was a bit confused what laminas-cli had to do with the tooling, at which point Max pointed out that laminas-cli already knows about both Mezzio and MVC configuration, and this would allow us to just create a command to expose to laminas-cli to do the work.
Marco thought that would be fine, and [Artem](https://github.com/zakirullin) (the individual proposing the RFC) indicated this was already his preference.

From here, we turned to the question of whether it should be shipped inside laminas-servicemanager, or in its own repository.
Consensus was to ship it as a separate package, and to keep the number of requirements as slim as possible.

We then held a vote, which passed unanimously.

Matthew worked with Artem immediately following the meeting to get the new repository ([laminas-servicemanager-inspector](https://github.com/laminas/laminas-servicemanager-inspector)) setup and registered with Packagist.
