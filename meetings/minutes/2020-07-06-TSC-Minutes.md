# Minutes from the 2020-06-01 Laminas Technical Steering Committee Meeting

- When: 2020-07-06 at 19:00 UTC, until 21:32 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brückner
  - Gary Hockin
  - Geert Eltink
  - James Titcumb (arrived towards end)
  - Luís Cobucci
  - Marco Pivetta
  - Max Bösing
  - Michał Bundyra
  - Matthew Setter (left early)
  - Matthew Weier O'Phinney

Quorum was met (11 out of 15 members were present at any given time).

## Agenda

- Discuss and evaluate moving components to security-only maintenance.
  ([jump to discussion](#evaluate-moving-components-into-security-only-maintenance))

  Marco, in conjunction with Gary, had [proposed a list of components to mark as
  only receiving security fixes](https://github.com/laminas/technical-steering-committee/pull/31).

- Call for maintainers.
  ([jump to discussion](#call-for-maintainers))
  
  - Is there a list of current maintainers?
  - If not, how could we provide information about our package maintainers?
  
  Currently, the only way a developer may become a maintainer of a package is
  that they have to contribute and be visible for the TSC. But what, if a
  package cannot evolve that fast? What, if there are plenty of developers who
  might want to apply as a maintainer to help out but don't know how (due to
  lack of ideas for new features or lack of bugs - which should be good tho
  ;-))?
  
  We should probably consider an application of developers where they choose
  their favorite package. Probably like a job application (which is actually
  volunteering). Probably, developers want to apply to a package which is
  (currently) unmaintained.
  
  But first of all, we might need a list of packages which are maintained and
  which are not. Having that list be publicly available and visible (either on
  github and/or on the laminas website) will help all (especially the TSC) to
  see where maintainers are needed.
  
  Having that list will also help (current and potential new) maintainers to
  have visibility of their voluntary efforts. They could use it while applying
  on new jobs or whatsoever.

- laminas-diactoros-serializer
  ([jump to discussion](#laminas-diactoros-serializer))

  [Matt Allan](https://github.com/matt-allan) recently [requested on the Diactoros issue tracker that we separate the serializer implementations into a separate package that uses PSR-17 factories to produce instances](https://github.com/laminas/laminas-diactoros/issues/43).
  This is something I (Matthew) have been considering for a while, and it was
  reasonably easy to do so:
  https://github.com/weierophinney/laminas-diactoros-serializer

  I'd like to bring this in under the Laminas umbrella, and then start working
  on deprecating the functionality in Diactoros (by first having our own code
  proxy to the new code).

- Adopt `doctrine/automatic-releases`?
  ([jump to discussion](#adoption-of-doctrine-automatic-releases))

  - demo
  - port to laminas organisation, adopt laminas license?
  - move it to GitHub actions
  - which user and GPG key should we use for releasing?
  - Is the brainching model suitable for laminas?

- Rename master branch?
  ([jump to discussion](#renaming-the-default-branch))

  In light of the recent societal focus on issues of racism and diversity, can
  we please adopt [more inclusive terminology as proposed to the IETF](https://tools.ietf.org/id/draft-knodel-terminology-00.html)?
  In particular candidates for change include renaming the "master" branch to
  "main" (per GitHub's own recommendations), and finding locations where we use
  terms such as "whitelist" and "blacklist" and renaming these.

## Focus on maintenance and maintainers

The originally stated agenda was:

- Call for maintainers
- laminas-diactoros-serializer
- doctrine/automatic-releases adoption
- renaming master branch
- BONUS ROUND: reviewing components to keep maintaining

We started discussing the call for maintainers, but between remarks by Max
around his rationale for raising the question (he is currently splitting
laminas-cache adapters into their own satellite packages, which will need
maintainers), and Luís ("It's easier to attract people to contribute when we're
specific regarding what they'd contribute to. It's kind of giving some
purpose."), we realized after 15 minutes of discussion that we needed to start
with the question: will we continue maintaining _everything_, or will we start
marking some packages as being in security-only maintenance?

### Evaluate moving components into security-only maintenance

Gary noted that we tend to spread ourselves thin by the very nature of the sheer
volume of packages we provide. Marco added that if we can mark repositories as
security-only, we can ignore new issues and patches against those repositories
when triaging issues and patches across the organizations we manage, making our
maintenance task less daunting. (Currently, deciding _where_ to spend your time
can consume as much time as any work you might do.)

The chief concern raised was the impact on users of marking things as
"unmaintained." The consensus was that we would craft verbiage for the
`README.md` of each such repository along the lines of "This package is
considered stable and receving security updates only," or "this repository is
only accepting essential security fixes for the foreseable future," possibly
adding verbiage to recruit maintainers for the repository. The idea would be
that if somebody wants to actively maintain the repository, they could request
to do so. In the meantime, leaving the repository unarchived simplifies the act
of applying security patches and issuing releases (should it be necessary), and
does not have the negative conntations of archiving (which implies it is
completely abandoned).

Aleksei indicated he felt _bugfixes_ should still be considered. Gary, Marco,
and Matthew pointed out that this would negate the entire idea of marking them
security-only, as we **would** need to monitor those repositories for issues and
patches. As Marco noted, "it's either world-breaking (security) or none" when it
comes to accepting patches to these repositories, _unless_ somebody steps up to
be a maintainer.

Luís jumped in with a question: "Let me invert this discussion, though. Instead
of talking about what could be possibly left unmaintained, do we have a clear
picture of what we definitely want to focus on?"

Matthew opened with "the middleware-related stuff (Mezzio, Diactoros,
Stratigility, and any related components such as developer-mode,
config-aggregator, etc.). Some of the core infrastructure pieces
(servicemanager, di, code, eventmanager). I'm up in the air about MVC; I know
some people swear by it and prefer it over middleware." Michał noted that when
we look at download stats, MVC has 10 times the downloads as Mezzio during this
past month, so we need to take into account not just what we are _interested in
maintaining_, but what the community is _interested in using_. Gary notes that
we should try and identify what _differentiates_ us from other projects, and
focus on that; for him, that's the middleware stuff. While those who use other
pieces might be disappointed, the point is to make a statement of intent: we're
not _abandoning_ anything, but we're _choosing to focus_ on other things.

> Editorial note: There were a number of suggestions for the _how_ of marking
> repositories as security-only. These included, but were not limited to:
>
> - Archiving the repositories (largely shot down for the negative
>   connotations).
> - Labeling them (via repository topics).
> - Using the bot to auto-close any issues/PRs opened against them.
> - Providing issue and PR templates that message that we do not accept new
>   bug reports or patches.

One last thing noted: Gary had an ulterior motive for this discussion: the new
release process (which is covered later). Rolling it out will be non-trivial,
and if we can reduce the number of repositories we need to roll it out to, we
will simplify this task for ourselves.

At this point, we held a vote: "Are we ok with restricting focus to just some
components?" The vote passed.

Matthew volunteered to pare down the original list (as we know some of the
components are under active development and have maintainers); from there, he
will start creating votes on each item in the list that the TSC can vote on
asynchronously.

### Call for maintainers

Now that we know we will be reducing our workload, the question is: how can we
make it easier for people to become maintainers, and to know it's even possible?

Aleksei suggested putting a badge on each page of the documentation, similar to
how we promote our CommunityBridge fund. A link in the README for each repo was
also suggested.

From here, we discussed a bit about how somebody indicates _why_ they want to
maintain a repository, and how they can demonstrate commitment. Aleksei
suggested that perhaps we accept applicants immediately, but put them in a
"triage" role at first. This would allow them to provide some immediate help
(labeling issues, verifying issues, reviewing pull requests), without being able
to do anything potentially problematic (merging incorrectly, merging code that
breaks backwards compatibility, etc.). The question was then raised of "how long
do they need to be in that triage role?" There was some discussion of a set time
period (e.g. 14, 30, or 90 days) or TSC meeting cycles as a way to set
expectations for users about when they will receive maintainer rights.

Luís raised a point: "I'm also assuming that there's some sort of 'mentor' for
those people." (Narrator: there is not!) This idea gained some traction
immediately, as it allows us to directly communicate what we expect out of
maintainers, and provide direct feedback as they do their triage work.

Since the by-laws already require a TSC vote to accept a new maintainer, we
decided on the following:

- We will create a document outlining expectations, responsibilities, and
  authority for maintainers.
- We will create a new issue type in the maintainers or TSC repository for
  applying to be a maintainer. The issue type will prompt for their github
  username, the repositories they want to maintain, their timezone (so we can
  match them to a mentor) and optionally some background on _why_ they want to
  do so.
- Collectively as a TSC, we will monitor for new applications, and volunteer as
  mentors when schedules fit; the fallback mentor will be the current project
  lead.

Max volunteered to draft the document and issue type, and several people
volunteered to provide feedback and assistance.

### Adoption of doctrine/automatic-releases

Marco and Gary have been working on extracting the doctrine/automatic-releases
workflow into a package which we could then fork and bring into the various
Laminas organizations and their repositories, ideally as a GitHub action or app.

They have previously recorded a demo video outlining how things work:
https://drive.google.com/file/d/1CH-Rry7trAdIkvFS5jpHhyHEDG4dugu1/view?usp=sharing

As a summary/recap:

- Everything release-related is directly managed via milestone.
- The tool (currently) operates under the assumption of 1.2.x , 2.0.x , master
  (for example) branching name.
- The tool creates tags and releases, reacting specifically to when a milestone
  is closed.
- The tool will create pull requests from stable branches to the next stable
  branch (1.2.x -> 1.3.x, 1.3.x -> master).
- The tool creates release branches.

As an example, consider a repository with the following branches:

- 1.0.x
- 1.1.x
- 1.2.x
- 1.3.x
- 2.0.x
- 2.1.x (no releases tagged from this branch yet)

If a bug is noticed in the 2.0.x branch, a patch is created against it and
assigned to a milestone representing the next version in that release series
(e.g., 2.0.3). When all issues and PRs related to that milestone are done, the
maintainer can then close the issue. When that happens:

- The tool tags version 2.0.3.
- The tool creates a release for version 2.0.3.
- The tool creates a pull request against the next newer release branch, 2.1.x.

At this point, the maintainer will then determine which milestone to add the new
PR to (likely 2.1.0), and merge it (resolving conflicts as necessary).

When all tasks for 2.1.0 are complete, the maintainer will close the 2.1.0
milestone. This will:

- Tag version 2.1.0.
- Create a release for 2.1.0.
- Create a new release branch, 2.2.x.

If we decide we do not want a 2.2.x series, and instead want a 3.0.x series, we
can rename that branch.

If a security issue is reported, we find the earliest version we still support
(which is based on the minimum PHP version supported in that branch). We create
the patch, assign it to a new milestone, and do the merge and close milestone
dance. In our example, if we started in branch 1.2.x, after merge, we would get
a pull request issued against the 1.3.x branch. We would assign, merge, and
close, wich would create a new 1.3 release and issue a pull request against the
2.0.x branch. Lather, rinse, repeat until we get to the newest release branch.

One question raised: how do we remove stale release branches (ones we no longer
support)? This is automation we can add as part of release tagging - identifying
stale branches and removing them.

Aleksei raised an objection, as his current process is to tag locally, and then
diff the new tag against the previous one before pushing it. Several of us noted
that this becomes `git diff <previous version>..HEAD` or `git diff <previous
version>..<release branch>`, issued prior to manually closing the milestone.

At this point, the discussion devolved into nit-picky implementation details
which we can sort out later.

We then voted: Shall we use the process outlined by Marco for automated releases
based on milestones? The vote passed.

Matthew agreed to setup a bot user and assign a GPG key to them. Marco will
finalize some work on the tool, and then bring it into the Laminas org as a new
repo. We will then develop a plan for rolling it out.

## laminas-diactoros-serializer

Matthew introduced a subcomponent he created based on user requests:
laminas-diactoros-serializer. The purpose is to split out the various utilities
for de/serializing PSR-7 messages to/from arrays and strings, and ship them in
such a way that they will work with PSR-17 factories (thus making them
independent of PSR-7 implementation)

Max noted he'd like to see interfaces created for serialization. Marco noted
that these might be better suited as hydrators/extractors. Aleksei asked if they
can create HTTP/2 messages as well as HTTP/1.1.

At this point, Matthew retracted any votes, so that he can start incorporating
the feedback and ideas provided.

## Renaming the default branch

Gary pointed out we'd skipped this item, and, despite the fact we were now 130
minutes in, we continued on.

The general gist is that the word "master" is problematic from a socio-political
perspective, and it disenfranchises and disincentivizes developers who have
historicaly suffered from slavery and/or segregation. Context-wise, with version
control, there are far more descriptive words we could use: "main", "latest",
and "trunk" are often suggested.

One member raised the question of whether "master" has associations with slavery
outside of the US. Several people noted that this is irrelevant; if we can make
a change that both prevents the negative connotations AND provides a better
convention for ourselves AND makes the community more welcoming, why would we
even entertain such a debate?

Marco noted that the new tooling is geared towards release branches, and that we
could easily have it mark a newly created release branch as the default branch
(Matthew verified that the API allows doing this). As such, we could eliminate
the branch entirely. This also has some benefits:

- no more need for "branch-alias" definitions
- clear communication of where a patch will land (the specific release branch
  chosen)

We opened a vote: "Shall we allow the release tooling to create a new release
branch and mark it as the default branch when a new minor or major release is
made?" The vote passed.

## Summary

This was a very long meeting (running 2.5 hours), but was a much-needed
discussion about how to make maintaining the project easier and more welcoming
for new contributors. We should start seeing the new release process roll out to
a select group of repositories in the near future, and have mechanisms in place
for developers to apply to act as maintainers, and gain mentors in the process.
