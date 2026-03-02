# Next Technical Steering Committee Meeting Agenda

- Date: 2026-03-02
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Integration with Valinor

[Marco Pivetta](https://github.com/Ocramius/) proposes introducing a new Mezzio to [Valinor](https://github.com/CuyZ/Valinor/) integration component.

Valinor is so incredibly central to modern PHP applications that rely on strongly typed DTOs for
inputs and outputs, that it is worth shipping an opt-in integration for it.

The integration layer would take an opinionated (but configurable) approach at converting request
objects into application- or domain-friendly DTOs, taking data from request QUERY, BODY or routing
parameters.

Things we need to fly over:

* [ ] should we build it, or is something out there already?
* [ ] development will be done on https://github.com/Roave/mezzio-valinor first, to validate the design assumptions
* [ ] are we OK with potentially moving such a component directly into Mezzio?
* [ ] are there long-term maintainability and security concerns? 
