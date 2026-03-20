# Minutes from the 2026-03-02 Laminas Technical Steering Committee Meeting

- When: 2026-03-02 at 19:00 UTC, until 20:15 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Aleksei Khudiakov 
    - Frank Brückner 
    - George Steel 
    - James Titcumb 
    - Julian Somesan
    - Luís Cobucci 
    - Marco Pivetta 
    - Matthew Weier O'Phinney
    - Michał Bundyra 

Quorum WAS met (9 out of 16 members were present).

## Agenda

### Integration with Valinor

Marco proposed to integrate Valinor into Mezzio via a layer that is opinionated and configurable.
The package is designed to convert request objects into application- or domain-friendly DTOs, taking data from request QUERY, BODY or routing parameters.

#### Discussion

Marco argued that the [cuyz/valinor](https://github.com/CuyZ/Valinor) library is very effective at converting HTTP payloads (and more) into usable data in common HTTP application scenarios.
He provided this simple example to outline the general usage to the TSC members for feedback.

```php
final readonly class AddToCart
{
    /**
     * @param non-empty-string $sku
     * @param int<1, max> $quantity
     * @psalm-suppress PossiblyUnusedMethod this constructor is only ever used by valinor
     */
    public function __construct(
        public string $sku,
        public int $quantity,
    ) {
    }
}

$app->post('/cart/{sku}', function (ServerRequestInterface $request) use ($mapper): ResponseInterface {
    $input = $mapper->map(AddToCart::class, $request);

    return new JsonResponse([
        'reached_endpoint' => true,
        'sku'              => $input->sku,
        'quantity'         => $input->quantity,
    ]);
});
```

Marco intends to make it work as a completely independent component at first, endorsed by Laminas.
Later on, it could be included in the Mezzio skeleton installation - installed by default, but excludable.

James, George and Matthew agreed that integrating the package sounds good.

#### Decisions

Marco offered to create a `mezzio-valinor` package to have it ready for the `cuyz/valinor` 1.0 release in the coming weeks.
Matthew created a poll to officially confirm the decision to integrate Valinor into Mezzio - it passed during the meeting.

### When will laminas-mvc be abandoned?

The original statement related to abandoning laminas-mvc is no longer correct, so a new date must be decided on to also allow time for users to migrate away from it.

#### Discussion

Marco worried that the news about abandoning laminas-mvc could spread fear among consumers.
He proposed to keep it available even past PHP 9 as an application that is functional, but no longer expanded.

Several members offered input that the maintenance for laminas-mvc is unfeasible:

- Aleksei mentioned that laminas-mvc is effectively abandoned, unless major updates and breaking releases are submitted.
- Julian confirmed that several of laminas-mvc's components will not support PHP 8.5.
- Matthew agreed that any component updates also require QA which adds a lot of work.
- Frank mentioned several more abandoned downstream dependencies within the Laminas ecosystem.

Though Marco offered to submit updates, as he has done with George's help, to maintain the application, he eventually agreed that the amount of work to keep laminas-mvc is too great.

The members agreed that the only solution forward for laminas-mvc users is to migrate away from it.
It would be impossible to create generic tooling for the migration.
The best solution is analyzing each project for migration by contractors and companies (like Roave and Apidemia) endorsed by Laminas.

Luís worried about the ethical side of TSC members offering paid-for-hire work to migrate from a tool that they abandoned.
Several other members agreed with this view, though they were also eager to help limit the impact on users.

#### Decisions

James will draft an announcement blog post to provide more information and a new date related to laminas-mvc's maintenance status.
Julian and any volunteers will work on migration guides.
Frank will update README.md files in the impacted Laminas packages.

