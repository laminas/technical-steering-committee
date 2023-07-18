# Minutes from the 2023-07-03 Laminas Technical Steering Committee Meeting

- When: 2023-07-03 at 19:00 UTC, until 20:20 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Alexei Khudiakov
    - Andreas Heigl
    - Gary Lockett
    - George Steel
    - Luís Cobucci
    - Marco Pivetta
    - Max Bösing
    - Michał Bundyra

Quorum WAS met (9 out of 15 members were present).

## Agenda

### Feasibility of adding RectorPHP to our workflow

RectorPHP has been used to assist with upgrading PHP versions in projects for some time and is closing on a 1.0 release.
Gary Lockett created a test PR for `laminas/laminas-diactoros` at https://github.com/laminas/laminas-diactoros/pull/163 in order to start gathering some feedback.

As a result Gary would like to discuss adding Rector to our workflow, whether it is feasible, worthwhile, and what our intentions would be with such a tool. The basic proposal would be that we add it to check for any instances of PHP code which can now be improved in newer versions, and automating that task.

### Discussion

Generally members met the proposal with enthusiasm and most discussion revolved around how to integrate the tool with the CI environment. Alexei Khudiakov raised concerns about running rector on submitted PRs as it may deter contributors.

Discussion focussed on possible integrations:

- A scheduled GitHub action to open a PR with blanket improvements
- Running a GitHub action manually, perhaps prior to release to identify possible improvements
- Using Rector's diff capabilities to annotate new PRs with improvements (without failing CI)

The discussion brought further urgency to implement Roave Backward Compatibility Check in the CI matrix to help prevent the introduction of breaking changes.

Ultimately, a vote was cast on whether to first introduce Rector as a scheduled GitHub action to the shared CI workflow which passed with 10 votes in favour, none against and no abstentions.

### Serializer component

As of the TSC from [2020-08-03](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2020-08-03-TSC-Minutes.md#vote-on-components-to-mark-as-security-only), the `laminas-serializer` component is marked as "security-only". Due to the way how it is used in other components such as `laminas-cache`, `laminas-hydrator`, `laminas-i18n` and `laminas-api-tools` components, it is not **that** easy to avoid this component at all.

Due to the release of `laminas-servicemanager` v4, almost **every** component needs new major versions (so does `laminas-serializer`). Having new major releases in "feature-complete"/"security only" packages feels kinda weird and thus, we should talk about how to proceed.

On slack, [Matthew](https://github.com/weierophinney) already stated two options:

- continue maintaining `laminas-serializer` due to the dependency issues with other components
- switch to other 3rd-party serializer (which would also include having multiple serializer interfaces around in multiple components)

The continuation of maintenance in `laminas-serializer` could be approached by dropping niche serializer implementations as stated in https://github.com/laminas/laminas-serializer/issues/21

Reducing the amount of serializers within laminas-serializer would reduce maintenance effort and thus, the project could remain in "feature complete"/"security-only".

#### Question

- Do we want to continue maintaining `laminas-serializer`?
- If the answer is `yes`, do we want to continue supporting niche serializers such as `PythonPickle`, `wddx`, etc.?

#### Discussion

Discussion was short on this subject with Max volunteering to maintain the component on the proviso that the niche serializers could be dropped in the next major release.

A vote to reinstate the package as a major dependency of `laminas-cache` passed with 8 in favour, 2 abstentions and 1 against.

### Fig Cookies Dependency

[dflydev-fig-cookies](https://github.com/dflydev/dflydev-fig-cookies) is used by a handful of Mezzio and Laminas components and seems to be un-maintained. It's currently holding back at least 2 packages from adopting `psr/http-message:2.0`: mezzio-authentication-session and laminas.dev - Obviously, `mezzio-session` depends on this package also, therefore, any Mezzio project that uses sessions is stuck on psr/http-message:1.0

- Does anyone know the maintainer, and can reach out to get this package updated?
- Is it desirable or feasible to fork, release and maintain in-house?
- Does anyone know of an alternative lib that solves the same problem that we could adopt instead?

#### Discussion

Discussion focussed on whether to fork the package or not with Max noting that it is a small problem domain. Ultimately, an informal decision was made to wait until the next TSC meeting to see if the current maintainer would respond to enquiries, with most members in favour of a fork if the need arose.
