# 2021-06-07 TSC Meeting

- When: 2021-06-07 at 19:00 UTC, until 20:48 UTC
- Attending:
  - Abdul Malik Ikhsan
  - Aleksei Khudiakov
  - Frank Brüchner
  - Geert Eltink
  - Luís Cobucci
  - Marco Pivetta
  - Matthew Setter
  - Matthew Weier O'Phinney
  - Max Bösing
  - Michał Bundyra

Quorum was met (10 out of 15 members were present).

## Agenda

### Enable Coveralls support in laminas-continuous-integration-action

The switch from Travis to Github Actions has seen Coveralls support not ported.

[Filippo Tessarotto](https://github.com/Slamdunk) asks to re-enable it: having the code-coverage feedback automation is a great value and helps maintainers evaluate pull-request validity.

Matthew began by noting that Marco had instructed him _not_ to include coveralls in the CI, with a plan to use something like [Infection](https://infection.github.io/), which he feels will give a far better idea of what code has been actually tested, and whether or not it has been coded correctly.
Marco noted during the meeting that refactoring often reduces coverage, making the tooling less useful.
Geert indicated that he's actually added useless tests just to keep the coverage numbers up.
Aleksei noted that he feels coverage focuses on testing HOW code works versus WHAT it should be doing, which often leads to bad design and issues later when refactoring.
Max noted that as we roll out more type hints and target Psalm as an essential part of our QA, we can actually remove tests that are no longer relevant — which can drive down coverage scores further, while actually improving quality.

Filippo indicated that as a maintainer:

- Infection requires a fair amount of knowledge to master how to approach issues it flags.
- Our Psalm baselines mask a lot of cruft currently.
- Coverage at least lets him know if new code is being tested.

A lot of back and forth then occurred, debating different coverage tools and the merits of them.
Matthew finally stepped in and pointed out:

> The goal is code quality, and making it easier for maintainers to know when a patch has test coverage.

And Luis reinforced that:

> I feel like we should be talking about the benefits we get from these tools instead of focusing on implementation cost.

Matthew noted that we have added Coveralls to a few repos via some of the pre/post hooks in the CI container, so Filippo can use that functionality for now for repositories he maintains.

Marco dug up how he does mutation testing on the automatic-releases repository, and noted that it setup to run on the diff only, and to report all mutations as comments on the patch.
Filippo agreed this is good, but also noted that some of the comments it makes would actually slow him down during review.
(Marco noted that the comment Filippo linked to actually _helped_ him in the review; clearly tooling usefulness varies based on the user!)

Luís jumped in to note that he's used mutation testing with code that had low coverage.
What he found was that it helped highlight issues in critical code paths, and helped prevent issues for them.
By having a requirement that the mutation score indicator should always be 5% improvement over the previous score for code they touched, his team was able to raise the mutation score indicator from 25% to 67% gradually.

At this time, we'd been meeting for over an hour, so Matthew summarized:

- We have ways to use code coverage tools with our repositories now via the pre/post run hooks in the CI action; maintainers who want to use those tools can do so already.
- We have general consensus that tools such as infection would give us better code quality in the long run, but need a concrete proposal for how to roll something like that out.

### Remove Line Length Limit from coding standard

[Maximilian Bösing](https://github.com/boesing) wants to drop the line length limit from the laminas-coding-standard ruleset.

He argues that the line length limit is counter-productive in combination with psalm and more precise argument-/return-type definitions, pointing to typehints like `array|iterable|ArrayIterator|ArrayConfig|WhateverArrayType` as leading to lines that exceed our line limits.
He argues that IDEs and editors have line wrapping for when the code does not fit on the screen, so line limits don't make a ton of sense.

Matthew noted that most of the cases where he's noticed this as he applies Psalm to repositories is around complex types, usually involving arrays or iterables, and that these can be wrapped over multiple lines to make them more readable anyways.
He also notes, however, that long test names are the ones where he hits the limit most regularly.

Geert notes that not everyone works on a big screen, and wrapping can make it harder to understand code flow as it breaks blocks in unexpected locations.
Aleksei notes that even the GitHub browser UI limits lines to 150 characters, and then requires horizontal scrolling to see the rest of the line; he also notes that even on a big monitor, 120 characters is an uncomfortable length for reading.

At this point, we dove into some history.
Some of the oldest coding standards mandated 80 character lengths, largely due to 80 characters being the standard width of a terminal screen.
PSR-2 indicated a "soft limit" of 120 characters, recognizing that 80 characters was often not enough, and that most terminals were resizable at this point.
It was marked as a soft limit, as there's a recognition that there are occasionally reasons to go over it.
The problem we have now is that it's treated as a warning, and even warnings will cause phpcs to fail.
Luís notes that the `-n` flag to phpcs will skip warnings, and that it can be configured in the `phpcs.xml.dist` file as well.

We had a vote at this point, with the following options:

- Keep the rules as-is.
- Bump the soft limit to 150 characters.
- Remove the line length rules entirely.
- Abstain.

We had 9 people voting; 4 voted to keep the rules as-is, 3 voted to increase the limit to 150; 1 voted to remove the line length rules; and 1 person abstained.
Since we didn't have a majority on any option, we kept the status quo.
