# Next Technical Steering Committee Meeting Agenda

- Date: 2024-07-01
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Laminas Bus Factor

Recently, 3 of the most skilled, knowledgeable and senior members of the TSC have signalled their intent to either scale back or withdraw from opensource. Without these TSC members, Laminas and Mezzio would be left with vanishingly small pool of maintainers, many of which have little of their own personal time to work on the projects.

Of the 17 members of the TSC, at least 4 of these could be considered inactive. Typically, there are around 9 members at monthly meetings; with 3 further withdrawals, and assuming current attendance levels, despite the huge loss of expertise, we would likely not have quorum at any future meetings.

The time it takes for PRs from existing members and contributors to get reviewed and merged is, in my subjective opinion, increasing. By no means should this be considered criticism of individual members - we are all people with lives to lead and personal responsibilities.

The question is what can be done to improve the situation?

Here are a handful of ideas that can hopefully be used as talking points at the next meeting:

- use accrued Laminas funds to pay for an existing member to spend time on Laminas
- consider ways to reach and recruit new maintainers
- remove members from the TSC that no longer wish to participate in order to make quorum easier to reach
- ask for commitments from existing members to perform maintenance duties for a small amount of time at regular intervals. For example, perhaps each member could commit to 2 hours per week/month _(at a convenient time)_ to dedicate to the projects, using that time to review patches, make CI green, whatever…
- survey existing members for nominations of new maintainers

As someone who uses Laminas/Mezzio in client work, I have a vested interest in seeing the components continue to evolve and improve - and I believe the projects are solid and viable alternatives to the other major frameworks. It would be a shame to witness the slow death of the projects…

### Licensing

The current state of open source is such that developers provide their time and expertise contributing to projects for no financial reward, whilst corporations reap the benefits by selling software and services built from those components for profit.

One way to redress this imbalance is via licensing - deny profit making enterprise access to software unless they pay for it.

- Is a discussion around re-licensing Laminas and Mezzio components worth having?
- Are there any existing licenses that could be adopted to improve outside investment?
- Could we use Laminas funds to pay for decent legal advice?
- Is potential non-use/reduction in use a concern?
- Would re-licensing be compatible with any constraints placed on us by the Linux Foundation?

### Extract Laminas Translator Interface to a new component

Introduce a new package `laminas-translator` that contains only the `LaminasTranslator` interface. Release 2 versions, v1.0 without native types and v2.0 with native types, i.e.

```php
namespace Laminas\Translator;

interface Translator
{
    /**
     * Translate a message.
     */
    public function translate(
        string $message,
        string $textDomain = 'default',
        string|null $locale = null,
    ): string;

    /**
     * Translate a plural message.
     */
    public function translatePlural(
        string $singular,
        string $plural,
        int $number,
        string $textDomain = 'default',
        string|null $locale = null
    ): string;
}
```

Implement this interface in `laminas-i18n` so that all other components that consume a translator can rely on the interface without depending on `laminas-i18n` - then, hopefully, we'll have an easier time upgrading to service manager v4 in those components.
