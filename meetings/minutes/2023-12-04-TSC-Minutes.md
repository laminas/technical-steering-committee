# Minutes from the 2023-12-04 Laminas Technical Steering Committee Meeting

- When: 2023-12-04 at 19:00 UTC, until 21:00 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
  - Aleksei Khudiakov
  - Andreas Heigl
  - Frank Brückner
  - George Steel
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Setter (came in at 20:49, so not counted towards quota)
  - Matthew Weier O'Phinney
  - Maximilian Bösing
  - Michał Bundyra

Quorum WAS met (9 out of 15 members were present).

## Agenda

### Maintainers for laminas-mime and laminas-mail

Slamdunk and settermjd have offered to maintain laminas-mime and laminas-mail; should we approve this, or mark laminas-mail as a security only package?

#### Discussion

The discussion was mainly around what laminas-mail _does_, and whether there are replacements for it in the ecosystem.
[Filippo Tessarotto](https://github.com/Slamdunk) pointed to:

- [ddeboer/imap](https://github.com/ddeboer/imap) for interacting with IMAP
- [zbateson/mail-mime-parser](https://github.com/zbateson/mail-mime-parser) for parsing MIME messages
- [symfony/mailer](https://github.com/symfony/mailer) for sending mail

Matthew asked about POP3, and the consensus is that it's not widely used anymore.

Matthew asked for clarification of the agenda item: is it to add a maintainer (Matthew Setter), or to mark the package security-only?

Aleksei pointed out that MIME has evolved over time, and we are quite behind.
On top of that, in his research, he discovered that the Thunderbird email client as 3 separate MIME parser implementations, due to the amount of different mail out there, which may or may not conform to different MIME-related RFCs.
His take is that it would be massive work to keep our own package up-to-date and secure.
Filippo seconded this, pointing out that zbateson/mail-mime-message (which he helps maintain) is very careful to point out that it can parse the message structure, but it's up to the person using the library to actually do something useful with it (which might include transforming it based on encoding).
Aleksei came back to point out that UTF-8 encoded subjects is one modern MIME capability we do not support, and these are very common today.

At this point, we held a vote to mark it security-only, but during the vote, there were suggestions we should maybe abandon these two instead.

After the security-only vote was completed (6 voted in favor, 2 abstained), Matthew asked if anybody would have changed their vote if it has been for abandonment.
One person said they'd have voted to abandon, whereas they'd abstained previously.
Aleksei indicated he'd have voted against.
When asked why, he pointed to the 13k daily installs as evidence it's in wide use.

Matthew indicated that he feels without anybody who can commit to maintaining it, and nobody on the team with security experience in this particular area, it may actually be a disservice to end users to commit to security patches.
Any non-trivial reports that come in could end up with no solution, or a solution that takes too long and/or requires BC breaks to be useful.

Aleksei agreed at that point, considering we have suggestions for replacements.

#### Decision

We will abandon laminas-mail and laminas-mime.
We will add recommendations to the three other projects in the README, and link to symfony/mailer for the "abandoned" property of the project.

Matthew will reach out to the Magento open source project and let them know, as they are one of the consumers of these packages. Done: https://github.com/magento/magento2/issues/39170

### BC Checks in the CI pipeline

Slamdunk requests that we add [roave/BackwardCompatibilityCheck](https://github.com/Roave/BackwardCompatibilityCheck) as a default job to be run in CI.

#### Discussion

Max indicated he already added support for this in the CI pipeline, but it's opt-in, via a configuration flag.
The concern with enabling it by default is that third-party users of our CI might suddenly get failing builds.
Marco suggests doing a new major release to enable it by default, and then we can gradually update our components to use the new major.
Max countered that we _could_ have Laminas-specific handling within our matrix generator to enable it.

This latter was met with some enthusiasm, as it would be in line with other checks (which are enabled only when certain conditions are met, such as configuration flag or a tool's config file being present).

#### Decision

After some back and forth, we decided on the following:

- Update the matrix builder _now_ to detect Laminas package names, and enable the checks if no config option was provided.
- Update the CI to allow org-wide configuration files; this will allow enabling/disabling at the org level.
- Release a new major of the CI that enables the check by default.

### Pimple service manager configuration

Should we abandon [laminas/laminas-pimple-config](https://github.com/laminas/laminas-pimple-config)?

- [Last release was in October 2021](https://github.com/silexphp/Pimple/tags)
- [Package stats laminas-pimple-config](https://packagist.org/packages/laminas/laminas-pimple-config/stats)
- Frank notes that the project is abandoned, and we could just mark ours as "security-only"; however, once we reach the last PHP version supported by Pimple, we may still need to abandon it.

#### Discussion

Andreas felt initially that if we can support it and Pimple is still being maintained, we should just mark it security-only.
Matthew pointed out that the project itself states that it is accepting no changes at this time, other than PHP version compatibility.
George then pointed out that the only installations currently are likely CI, due to how few there are.
And the Aleksei pointed out that laminas-auradi-config is in a similar position, but worse, as Aura DI does not yet even support PHP 8.2.

At this point, folks suggested abandonment.


#### Decision

We voted to abandon both laminas-pimple-config and laminas-auradi-config.


### PHPCS is being abandoned/forked

For more context, [see this issue](https://github.com/squizlabs/PHP_CodeSniffer/issues/3932) by [@jrfnl](https://github.com/jrfnl), which effectively announces the fork and the probable (?) abandonment of the source package.

[Slevomat CS has indicated they will switch to the fork](https://github.com/slevomat/coding-standard/issues/1640). 

#### Discussion

Michał noted that there's not much to discuss at this point.
The phpcs community is largely planning to switch to the fork, and his own rulesets will adopt it as soon as the first tag is released.
We just need to wait, and then we should be able to update to the new package immediately within laminas-coding-standard, as the only change that affects us is the package name itself.
