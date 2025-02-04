# Minutes from the 2025-02-03 Laminas Technical Steering Committee Meeting

- When: 2025-02-03 at 19:00 UTC, until 20:25 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Aleksei Khudiakov
    - George Steel
    - Julian Somesan
    - Luís Cobucci
    - Matthew Setter
    - Matthew Weier O'Phinney
    - Michał Bundyra

Quorum WAS NOT met (7 out of 16 members were present).

## Agenda

### Major release for laminas-session

In order to implement servicemanager v4, a new major release for the laminas-session package version is required.
See PR's: https://github.com/laminas/laminas-session/pull/102 and https://github.com/laminas/laminas-session/pull/103.

In the current bugfix release, all functions that will be removed in V3 were marked as `@deprecated`.

#### Discussion

Matthew WOP, George, Julian and Aleksei agreed that a major release is necessary.
Julian mentioned that the issue breaking backward compatibility is the upgrade to laminas/laminas-servicemanager v4.
The package laminas/laminas-session is preventing other packages from using service manager v4.
Aleksei added that most Laminas packages also need their service manager updated to v4.

#### Decisions

The members agreed on a major release for laminas-session.

### Email accounts @getlaminas.org

Would email solutions from Tuta be beneficial?
https://tuta.com/blog/tutanota-for-open-source-teams

#### Discussion

The members discussed the need for member accounts on domain getlaminas.org, but didn't find a proper use for it at this time.
Matthew WOP mentioned that emails for security and marketing are already set up with forwarding to multiple members.

#### Decisions

The matter is postponed until a need for the feature arises.

### Dropping Support for PHP 8.1

@gsteel proposes to drop support for PHP 8.1, to upgrade to Psalm v6 and PHPUnit v11.

#### Discussion

Matthew WOP and Aleksei agreed that PHP 8.1 is still being supported, so removing it from Laminas packages would impact users.
Julian considered targeting PHP versions 8.2 to 8.4 for major releases, but changed his mind in favor of keeping support for PHP 8.1.
George argued in favor of keeping up to date with critical development tools, even if it meant dropping PHP version 8.1.
He wanted to take advantage of Psalm version 6 and the upcoming PHPUnit version 12.
Support for PHPUnit v10 ends in February 2025 and for PHPUnit 11, in February 2026, but Matthew WOP argued that PHPUnit's EOL for versions 10 and 11 are not determined yet.
He added that keeping support for PHP version 8.1 for the users of Laminas components outweighs the benefits of updating the development tools.
Aleksei further added that the versions for dependencies affect the version ranges in CI.

#### Decisions

Support for PHP 8.1 will be kept for now.

### New design and layout

Based on the current visual identity, @arhimede proposed a new design and improved layout.
https://github.com/laminas/getlaminas.org/issues/242

#### Discussion

Several members praised the new design forwarded by Julian's designer.
Julian mentioned that the goal is to have a more modern design to match the sites for other frameworks.
[This RFC](https://github.com/laminas/getlaminas.org/issues/242) is available for any input from the members.

#### Decisions

The members agreed to start work on the new design without the need for a vote.
