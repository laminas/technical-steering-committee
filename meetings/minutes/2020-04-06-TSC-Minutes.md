# Minutes from the 2020-04-06 Laminas Technical Steering Committee Meeting

- When: 2020-04-06 at 19:00 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Aleksei Khudiakov
  - Frank Brückner
  - Geert Eltink
  - Matthew Weier O'Phinney
  - Michał Bundyra
  - Rob Allen

Quorum was met (6 out of 10 members were present).

## Agenda

- Vote on new members:
  - [Abdul Malik Ikhsan (@samsonasik)](https://github.com/samsonasik) (nominated by @weierophinney)
  - [Luís Cobucci (@lcobucci)](https://github.com/lcobucci) (nominated by @weierophinney)
  - [Maximilian Bösing (@boesing)](https://github.com/boesing) (nominated by @weierophinney)
  - [Witold Wasiczko (@snapshotpl)](https://github.com/snapshotpl) (nominated by @weierophinney)
- CLI tooling for Laminas MVC, Mezzio, components
- Full example / demo applications
  - developed under https://github.com/laminas-tutorials
  - follows best practices and implements typical features
  - basis for new tutorials
- Opcache Preloading for MVC, Mezzio
  - @weierophinney has done some research, and posted an RFC for discussion:
    https://discourse.laminas.dev/t/rfc-opache-preloading-for-mezzio-and-mvc/1442
- Security Group
  - @weierophinney has setup the security@getlaminas.org email, but we need a
    new security group, as the bulk of those previously on it are either inactive
    or left the TSC. Who should get these emails?
- Where to post information?
  - There's been a few indications that cross-posting the Discourse topics to
    Slack may be unwanted.
  - But one reason for having the Discourse cross-posting is to make people
    aware it exists.
  - What is the consensus?

## New Members

We voted on each of the proposed new members (
  [Abdul Malik Ikhsan (@samsonasik)](https://github.com/samsonasik),
  [Luís Cobucci (@lcobucci)](https://github.com/lcobucci),
  [Maximilian Bösing (@boesing)](https://github.com/boesing), and
  [Witold Wasiczko (@snapshotpl)](https://github.com/snapshotpl)
), and each was unanimously approved.
Matthew will reach out to each to get formal acceptance, and then add them to
the #technical-steering-committee channel and each organization.

## CLI Tooling for Laminas MVC, Mezzio, components

Michał has proposed a new component, laminas/laminas-cli, which would provide
scaffolding for using a PSR-11 container containing a `config` service that
futher has a `laminas-cli` key with information on how to map CLI commands to
classes and/or services exposed by the container. This information, along with
the container, would seed a [symfony/console](https://symfony.com/doc/current/components/console.html)
application. The result would be that we could then expose commands from any
component using a single vendor binary.

We would ship the new component in skeleton applications by default.

The consensus was that this sounded like an excellent idea, as it would simplify
our console tooling story, and make it far easier for us to start exposing more
CLI tooling to users.

The main point of contention during the discussion was the naming of the binary.
Michał felt strongly it should match the name of the package. Everybody else
contended that since it is the console entry point for all components, it should
match the project name (i.e., "laminas").

### Summary

We voted unanimously to bring the new component into the Laminas organization,
with the caveat that the binary it exposes should be called "laminas". We will
update the Mezzio tooling to act as an alias to the new command, and start
adapting other components that expose CLI commands to expose them via the new
tool.

## Full example / demo application

Frank had added this agenda item, and indicated he started thinking on it when
Aleksei created the laminas-tutorials organization last year. The idea would be
to create a new tutorial or set of tutorials that build off of each other in
order to gradually demonstrate all features of the framework, similar to the
[Symfony demo application](https://symfony.com/blog/introducing-the-symfony-demo-application).

The idea would be to provide both the tutorials **and** the entire code, to
allow users to code along at their own pace, but then check what they do against
the reference application. The tutorial and code would cross-link to each other,
so that users can understand where in the tutorial code was added, as well as
jump to the code to see the rest of the context.

Rob indicated that he'd like to see multiple demo applications, as the
approaches and needs for an API differ from a website with sessions and HTML.

Aleksei noted that he feels a generic demo app is not enough like a real
application to be a good guide for all levels of experience.

### Summary

The one vote related to this topic was whether or not to bring the
laminas-tutorials organization under the Laminas Project umbrella; the vote was
unanimously in favor. Matthew will work with Aleksei to add the TSC team to the
organization.

## Opcache Prelaoding for MVC, Mezzio

Matthew had posted an [RFC for providing Opcache Preloading
tooling](https://discourse.laminas.dev/t/rfc-opache-preloading-for-mezzio-and-mvc/1442).
He'd had no feedback, so he started discussion by asking whether he should try
and get more feedback, or if the TSC would want to vote on starting work on a
prototype.

Consensus was that we would definitely want such tooling, and that it should
likely build on the newly approved laminas-cli component. Some input was also
provided indicating that post-generation, it should detail what needs to happen
to enable opcache preloading, and/or provide a command for spitting out a line
to append to a `php.ini` file. Additionally, there was a recommendation to use
the same file naming convention used by other frameworks if at all possible.

### Summary

The members present voted unanimously in favor of beginning a prototype
immediately. Matthew will work this into his schedule.

## Security Group

We had two vulnerabilities reported this past month, which brought to light that
we do not currently have a security group in place. As of this writing, Matthew
receives emails to the security@getlaminas.org account, brings the information
to the TSC, and then handles communication with the reporter and updating the
website when patches are available.

His question was: does this process work, or do we want to create an actual
security group?

During discussion, we uncovered that many are uncertain if they'd be able to
provide meaningful support, and others indicated their availability is limited.
Nobody volunteered to be on an inaugural security group.

### Summary

We'll leave the status quo, which is:

- Matthew receives security-related communications and reports them to the TSC.
- TSC members decide amongst themselves who will work on verification and mitigation.
- Matthew will communicate with the reporter and handle announcing advisories.

## Where to post Discourse information

Several TSC members and community members have indicated that they find the
cross-posting of Discourse topics to Slack noisy and unwanted. Matthew noted
that the reason to cross-post to Slack is largely to ensure that Slack users are
aware the forums exist in the first place.

Possibilities for improvement that were discussed included:

- Moving all Discourse posts to their own channel, like we do GitHub
  notifications. Rob pointed out nobody would likely subscribe to that channel,
  eliminating the usefulness of cross-posting in the first place.
- Elminiating cross-posting entirely.
- Providing a daily digest. Matthew indicated this would pose a fairly heavy
  development task, as we currently have no persistence capabilities.
- Truncating Discourse messages so they are not quite as noisy.

Matthew pointed out that while we direct users towards Discourse on an
individual basis, these messages get lost; having the cross-posts serves as a
reminder that the location exists, hopefully nudging users to search for answers
there, or even post there if they find no answers. Several TSC members pointed
out that having a channel such as #qanda sends a signal to users that Slack is
the right location to ask questions, and perhaps we should eliminate that. This
also raised the point that we might want to reorganize and slim down the number
of channels we have to encourage Slack as a place to discuss development, and
Discourse as a place to ask questions.

We also discussed how we might better draw attention to the forums for both new
Slack users, as well as existing ones, but had no clear ideas presented.

### Summary

We ended up holding two votes on this topic:

- Whether or not to kill the #qanda channel. Atending members voted unanimously
  to kill it. Matthew will follow up after the meeting to archive the channel.

- Whether or not to truncate Discourse topics posted to Slack. Attending members
  voted unanimously in favor of truncation.

Matthew will take care of the message truncation, and also attempt to add some
logic to only post new topics, and not comments on them.

We will discuss Slack channel reorganization at a later date; we would benefit
from having a concrete proposal in place to start discussions.

## Conclusion

The meeting lasted approximately 100 minutes, and we had broad consensus on all
measures taken.

The next meeting will occur at 19:00 UTC on May 4, 2020.
