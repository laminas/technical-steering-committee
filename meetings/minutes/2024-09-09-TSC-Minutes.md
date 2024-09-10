# Minutes from the 2024-09-09 Laminas Technical Steering Committee Meeting

- When: 2024-09-09 at 19:00 UTC, until 21:15 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Maximilian Bösing 
  - Luís Cobucci
  - Abdul Malik Ikhsan  
  - Gary Lockett
  - Aleksei Khudiakov 
  - Julian Somesan
  - George Steel
  - James Titcumb 

Quorum WAS met (8 out of 16 members were present).

## Agenda

### Laminas Ecosystem

As per [the RFC](https://github.com/laminas/getlaminas.org/issues/199), should we create Middleware and Wrapper sections for approved 3rd-party components on the getlaminas.org website?

#### Discussion

George was in favor, but worried about the maintenance effort.
Gary was also in favor and mentioned adding guidelines.
The attendees considered these possible guidelines:
- include components that are used internally
- include components are actively maintained, with some history behind them
- add a mailing list
- recheck the curated list every 2 months
- clearly flag components for removal
- group the components in categories 

#### Decision

The attendees agreed the section is useful, but did not hold a vote.
It was agreed to bring the matter up in the next meeting.
The primary categories will be Middlewares, Packages, MVC Modules.
The details on this item are subject to change based on future PRs.

### Proposal for new Maintainers

Postponed until the next meeting.

### Clarify maintainer's duties

Based on [the RFC](https://github.com/laminas/technical-steering-committee/pull/193), define what maintainers are expected to do and the minimum requirements to become a maintainer.

#### Discussion

Aleksei mentioned these items as being relevant for maintainers:
- managing direction of the component development
- maintenance and development work of the component
- triage of issues and handling contributions
- guidance of the contributors

The members considered the evolution of a developer from contributor, to maintainer, to TSC member. There was some disagreement on the definition of 'active member'. Aleksei argued that some current maintainers aren't active enough or at all. Eric worried that the bar for 'active' is set too high, making it difficult to be considered 'active'.

#### Decision

It was agreed that considering the nomination of maintainers is subjective, based on their activity in Slack, PRs, new issues, adding comments.
The TSC members will analyze said activity for future maintainers, since simply counting contributions from a developer is not reliable.

### Presentations (slideshow)

The site will enable the creation of official presentations to be used in conferences, user groups, ad-hoc presentations related to Laminas project.
It will also enable the collection of feedback before a presentation is published. 

#### Discussion

The general idea of presentations was embraced by the members.
The goal of the presentations was soon defined as a means for creating awareness about the Laminas project, even if done by non-Laminas members.

The members discussed the lack of any official Laminas speakers and the legal issues behind the branding of presentations as official Laminas marketing material. 

Regarding hosting, the members considered GitHub and getlaminas.com.

#### Decision

No decision was made. The matter will be discussed in the next meeting.
