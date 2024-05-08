# Minutes from the 2024-03-04 Laminas Technical Steering Committee Meeting

- When: 2024-05-06 at 19:00 UTC, until 19:53 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Gary Lockett
  - George Steel
  - Luís Cobucci
  - Matthew Weier O'Phinney
  - Max Bösing
  - Rob Allen

Quorum WAS NOT met (6 out of 15 members were present).

## Agenda

### Api-Tools related (proposed by Dotkernel organisation)

- Continuation of [discussion from April 2023](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2023-04-03-TSC-Minutes.md)

- What was changed in Dotkernel organisation related to API since that discussion:
  - There is a new dedicated website only for Dotkernel API, which is our main focus [dotkernel.org](https://www.dotkernel.org/).
  - There is now compiled, up-to-date documentation, for the API and all components and libraries: [docs.dotkernel.org](https://docs.dotkernel.org/).
  - It has integrated the [Laminas CI](https://github.com/marketplace/actions/laminas-continuous-integration) in all components and libraries.
  - All of the above are still a work in progress, in beta stage.

#### Proposal

1. Mark **api-tools** and all its components as archived in packagist and in github 
2. Remove **api-tools** from [getlaminas.org ](https://getlaminas.org/)
3. Replace **api-tools** with *Dotkernel API* on getlaminas.org website
   **OR** 
4. Recommend *Dotkernel API* as a replacement for **api-tools**

#### Discussion

There was no real disagreement with this proposal.
The main concern was about the migration path for users on Laminas API Tools to Dotkernel, as Dotkernel uses PSR-15 (via Mezzio), vs Laminas MVC.
Julian Somesan (speaking on behalf of Dotkernel) indicated that his team can build such tooling and/or documentation to facilitate migrations.

The main discussion was around the _logistics_ of this change, with a number of items highlighted:

- We will need to modify the getlaminas.org website to move links to Laminas API Tools to less prominent positions, with verbiage that it is no longer under development.
- We would need to provide links and recommendations for Dotkernel from the getlaminas.org website, for developers interested in API development.
- We will need to update the landing page for docs.laminas.dev to note the status of Laminas API Tools in its card.
  - Related, this would be another place to link to the Dotkernel project, likely directly to documentation.
- We will need to update each Laminas API Tools repository:
  - With a message on the `README.md` indicating deprecation status, and linking to Dotkernel as an alternative.
  - With the addition of the `abandoned` field in `composer.json`, pointing to Dotkernel
  - Optionally with the addition of a `_comment` field to detail that Dotkernel is not a 1:1 replacement, and pointing to an announcement elsewhere.
  - After the above changes are made, we could optionally archive each repository.
    The downside to this is that users will not have the ability to raise issues, which is a good place to push them to alternatives.
- We should create a blog post with messaging around the change.

Because we did not have quorum, Matthew indicated he will do an async vote of the TSC to ensure there's agreement for the general idea of abandoning Laminas API Tools and recommending Dotkernel API.

### Business presence 

Julian Somesan writes: Right now it seems that the website *getlaminas.org* as a presentation website looks kind of rusty and not updated.
The Dotkernel team  can allocate few hours of development and design on it. 
   
- Referring to this project, where there are some *Draft* ideas https://github.com/orgs/laminas/projects/23
- Also I want to push this RFC for approval:  https://github.com/laminas/getlaminas.org/issues/162
- And few more business related ideas which I can add to the above RFC afterwards

#### Discussion

Matthew noted that Frank Brückner has been sharing some design updates with him already, and asked Julian to coordinate with Frank.
