# Minutes from the 2023-04-03 Laminas Technical Steering Committee Meeting

- When: 2023-04-03 at 19:00 UTC, until 19:58 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Alexei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - Gary Lockett
  - George Steel
  - Luís Cobucci
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra

Quorum WAS met (11 out of 15 members were present).

## Agenda

### Nomination of DotKernel team members to join Laminas organization:

As per this [recommendation](https://github.com/laminas/technical-steering-committee/issues/135) from last TSC meeting, [arhimede](https://github.com/arhimede) nominated the following developers:

- [arhimede](https://github.com/arhimede)
- [alexmerlin](https://github.com/alexmerlin)
- [MarioRadu](https://github.com/MarioRadu)

Since then, each of these members has contributed to a Laminas package of their choice. Below, you can find their pull requests:

- arhimede: https://github.com/laminas/laminas-paginator/pull/56
- alexmerlin: https://github.com/laminas/laminas-json-server/pull/33
- MarioRadu: https://github.com/laminas/laminas-migration/pull/76

#### Discussion

Matthew W. noted on opening discussion that based on Laminas policies, this isn't really enough yet; the TSC requiers a _history_ of pull requests in order to evaluate maintainer access.
Julian (arhimede) immediately noted that he is aware that he and his team need to do more pull requests

Aleksei also noted that the maintainer role is given for specific components and repositories, with the TSC acting as fallback maintainers for the whole organization; based on the agenda item, he's not entirely clear what the DotKernel team is specifically wanting to maintain, particularly as they have mentioned "laminas-api-tools" in the request, but DotKernel focuses on Mezzio.
Julian clarified they want to help maintain the various repos related to API _tooling_ for Mezzio; in discussion, this means for them the various components that DotKernel already consumes or extends.

Gary L. asked if we should create a "mezzio-api-tools" or similar organization, and move some of the DotKernel repos there.
Max pointed out that we discussed this in the March 2023 TSC meeting, and that this would then mean even MORE repositories for Laminas to maintain, which is not feasible currently.
At this point, Matthew W. noted that this is essentially the next agenda item, and we moved on to that one.

### Move DotKernel API under Laminas vs keep under DotKernel organization

During the last TSC meeting (edit: 2023-03-06) the idea of moving [DotKernel API](https://github.com/dotkernel/api) under Laminas organization has been raised.

This idea should be discussed further in this meeting.

[Here](https://www.dotkernel.com/dotkernel3/dotkernel-api-architecture-components/) you can read more about DotKernel API.

#### Discussion

Andreas raised the idea of a separate API tooling org under the Laminas umbrella, but independent of the Laminas TSC.
Matthew then summarized the points from the March 2023 meeting, as what Andreas was suggesting was not dissimilar to previous discussions:

- We bring in DotKernel to Laminas.
  The TSC was mostly against this because (a) we're already spread thin, and (b) Apidemia can likely provide better focus and responsiveness maintaining DotKernel outside of Laminas.
- However, it may make sense to have them propose specific, more generalized components to us in the future.
- And potentially for members of DotKernel and/or Apidemia to help maintain existing components.
- Finally we also discussed the idea of promoting DotKernel to Mezzio users who want to build APIs, as it has a nice, integrated stack for that.

He then further asked the following of those present in the meeting:

- Why do you want it under the Laminas umbrella?
  Would cross-promotion be sufficient for your needs?
- Can we (the Laminas TSC) take on the extra admin of bringing these in, particularly as none of us are yet familiar with the code?

Julian answered that putting it under the Laminas umbrella brings more eyes and advice on architecture to DotKernel, which will help it become a better quality tool.
He also feels the project would have a better reputation if under Laminas.

Several folks chimed in that they have found themselves recreating the wheel on multiple API projects, and Julian pointed out that this was exactly what motivated the creation of DotKernel.

Andreas felt that rebranding it under Laminas might give the impression that the Laminas TSC created the project, which could be misleading.
However, pointing folks to DotKernel FROM Laminas would be relatively low effort, and an _endorsement_ of the project, which might help achieve many of their goals.

Max pointed out that while DotKernel does provide a fair bit of convenience, his main issue with it is that many of the packages _do_ lock you into the Mezzio/Laminas ecosystem.
As a developer, he tends to prefer packages that interface with standards and do not provide vendor-specific lock-in; doing so allows exchanging one package for another later.
Julian notes that this is something they could look into.
That said, Gary L. notes that he doesn't necessarily see this as problematic; one reason for Apigility's popularity was precisely that it was opinionated.

Matthew W summarized the discussion as follows:

- There's definitely some enthusiasm for the idea of DotKernel joining Laminas, however...
- TSC members would like more time to get to know the project and provide some guidance around architecture (particularly where there are duplications and/or hard-coded bindings), and
- Would like some time to see and evaluate contributions from DotKernel developers so that (a) TSC members are comfortable with their contributions, and (b) DotKernel developers are familiar with and comfortable with our processes.
-
Where this leads is still in the air: whether Laminas would adopt DotKernel, or would recommend it to users.
We decided we'd so some regular check-ins during TSC meetings over the coming months to see how the relationship between the projects is developing.
