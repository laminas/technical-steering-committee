# Minutes from the 2024-10-07 Laminas Technical Steering Committee Meeting

- When: 2024-10-07 at 19:00 UTC, until 20:39 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Abdul Malik Ikhsan
  - Frank Brückner
  - Gary Lockett
  - George Steel
  - Julian Somesan
  - Luís Cobucci
  - Matthew Setter
  - Matthew Weier O'Phinney

Quorum WAS NOT met (8 out of 16 members were present).

## Agenda

### Proposal to have a separate committee for marketing and outreach

In [the marketing-and-branding channel](https://laminas.slack.com/archives/C014W19NPV3), there have been discussions, recently, about how to help build awareness of the Laminas project, as well how we should approach marketing, branding, and outreach efforts. A proposal was put forward to have a committee separate to — yet which still overlaps and is answerable to — the TSC, which is directly responsible for these activities. This would allow those activities to happen in tandem to technical development of the project, while allowing those members of the TSC who aren't interested in these kinds of activities not to have to be involved with them.

#### Discussion

Luís asked what problem is being solved by creating another committee?
Julian indicated that the current TSC decision process is too slow for marketing efforts, and Matthew pointed out that currently some decisions require TSC intervention (e.g, if money is involved).
Gary asked if there are any specific examples, trying to determine if this is an existing problem, or a perceived problem.

At this point, the discussion turned to what the participation criteria and scope for the committee would be.
Julian suggested that the criteria currently is if somebody has expressed any interest in helping out in that way.
He suggested that the committee could involve non-TSC members as well.
Eric Richer asked if the point right now is to gauge interest in the idea first, and then create a full plan.

We had a bit of a sidetrack at this point when Gary Lockett suggested maybe having community managers instead.
He'd seen Satisfactory recently, and felt that their community managers did an excellent job in handling a variety of public-facing tasks, and that an approach like this might be effective for us.

Luís brought us back around to asking if we should have a _plan_ first, to ensure that we don't just blindly sign on to something without having evaluated it.
Julian suggested we have an unoffical MC to begin: try something, and then have a plan.
Luís countered that maybe we instead have a short-term trial that's time-limited, allocates some initial funding, and has actual success criteria; this would help us understand if the approach will work, and give us some data on how to move forward.
Eric suggested that the TSC draft this.

Julian then said that his biggest concern currently is the website, and getting changes in place.
Frank said this should not be a problem, and that PRs are all that are required.

#### Decisions

Matthew summarized the discussion:

- Julian would like faster pace for getting website changes in. Frank says "no problem".
- There may be additional efforts to take on the marketing front, but we need a plan.
- Luís suggests that we come up with a short-term, achievable plan with concrete outcomes for a marketing committee so that we can see if it will be effective, after which we can come up with a longer term plan.

### Proposal to hire a dedicated developer 

[Julian Somesan](https://github.com/arhimede) is proposing the below:

In the current open-source software ecosystem, the projects have became increasingly complex.
Becoming a contributor and maintainer for Laminas Project in particular is overly complicated, but willing developers are needed to push things forward.
There are months-old open issues and pull requests across their many repositories.
Apidemia, as official Laminas commercial vendor, proposes to hire [Alexis Karajos](https://github.com/alexmerlin) as a part-time employee (2-3 days per week) of Laminas Project.
In recent months, Alex Karajos, a valued and experienced employee of the Apidemia organization, has proven himself a capable contributor to several Laminas components.
Apidemia is willing to offer Alex's services for free, as an open source sponsorship.
Alex's purpose will be to manage open items and improve development flow across Laminas components.

#### Discussion

Julian noted that we have 359 open PRs in the Laminas org and 91 in the Mezzio org at this time, and the goal is to reduce that.
Matthew pointed out that we need to ensure that we've had a chance to review the reviewer: ensure that they are looking for the same things we are, and that they are collaborating well with contributors.
Julian pointed out that this person has been doing that for the last couple months.
George pointed out that he's been shadowing Alex already, but feels like he hasn't seen enough to consider them ready to do merges.
Julian indicates that at this stage, Alex would not close anything on his own, but would ask for a second opinion first.
Luís suggested adding triage rights for Alex as an initial step as well, and folks agreed this would be helpful in gauging his capabilities.

#### Decisions

We decided to give Alex triage rights to both the Mezzio and Laminas organizations, and will continue shadowing them to ensure they are delivering quality reviews and feedback.
