# Next Technical Steering Committee Meeting Agenda

- Date: 2020-07-06
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to discuss

- Call for maintainers
  
  Lets talk about maintainers. 
  
  - Is there a list of current maintainers?
  - If not, how could we provide informations about our packages maintainers?
  
  Currently, the only way how a developer may become a maintainer of a package is, that he has to contribute and be visible for the TSC. But what, if a package cannot evolve that fast? What, if there are plenty of developers who might want to apply as a maintainer to help out but don't know how (due to lack of ideas for new features or lack of bugs - which should be good tho ;-))?
  
  We should probably consider an application of developers where they choose their favorite package. Probably like a job application (which is actually volunteering). Probably, developers want to apply to a package which is (currently) unmaintained.
  
  But first of all, we might need a list of packages which are maintained and which are not. Having that list be publicly available and visible (either on github and/or on the laminas website) will help all (especially the TSC) to see where maintainers are needed.
  
  Having that list will also help (current and potential new) maintainers to have visibility of their voluntary efforts. They could use it while applying on new jobs or whatsoever.

- laminas-diactoros-serializer

  Somebody recently [requested on the Diactoros issue tracker that we separate the serializer implementations into a separate package that uses PSR-17 factories to produce instances](https://github.com/laminas/laminas-diactoros/issues/43).
  This is something I (Matthew) have been considering for a while, and it was reasonably easy to do so:
  https://github.com/weierophinney/laminas-diactoros-serializer

  I'd like to bring this in under the Laminas umbrella, and then start working on deprecating the functionality in Diactoros (by first having our own code proxy to the new code).

- adopt `doctrine/automatic-releases`?
   
   * demo
   * port to laminas organisation, adopt laminas license?
   * move it to GitHub actions
   * which user and GPG key should we use for releasing?
   * Is the brainching model suitable for laminas?

- rename master branch

  In light of the recent societal focus on issues of racism and diversity, can we please adopt [more inclusive terminology as proposed to the IETF](https://tools.ietf.org/id/draft-knodel-terminology-00.html)? In particular candidates for change include renaming the "master" branch to "main" (per GitHub's own recommendations), and finding locations where we use terms such as "whitelist" and "blacklist" and renaming these.
