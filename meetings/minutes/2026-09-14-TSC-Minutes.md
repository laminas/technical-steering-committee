# Minutes from the 2026-09-14 Laminas Technical Steering Committee Meeting

- When: 2026-09-14 at 19:00 UTC, until 20:05 UTC
- Where: Laminas Slack #tsc-meeting channel
- Attending:
    - Abdul Malik Ikhsan
    - Julian Somesan
    - Luís Cobucci
    - Rob Allen
    - George Steel
    - James Titcumb
    - Frank Brückner

Quorum WAS NOT met (7 out of 16 members were present).

## Agenda

### StructArmed for Architecture Guarding

#### Discussion

Abdul described StructArmed as an architecture-guarding tool that can also act like Rector (handling deprecation-style rules, e.g., flagging never-extended classes as `final`).
He demoed it and shared demo PRs against laminas-diactoros and mezzio, noting it ran on 2,215 files (Spiral framework) in 0.6 seconds.
Other members compared it to Deptrac, PHPStan.
George questioned whether an architecture tool is really needed for libraries (vs. applications).
Tyrsson noted overlap with **mago**, which also offers guard functionality.
Rob said he's tool-agnostic but favored adopting StructArmed, suggesting starting with a simple ruleset and expanding over time.

#### Decisions

The members agreed to move forward with StructArmed, starting simple and iterating.
George said the prerequisite is CI matrix support (to minimize YAML config) before rollout, and offered his recent Mago patch to laminas-ci-matrix-action as a template.
The plan is to update the CI action to detect the presence of `structarmed.php` (mirroring how it detects `mago.toml`) and run it automatically.
Abdul will draft a PR to laminas-ci-matrix-action for george to review.

### Other Items

George mentioned that `input-filter` still has unfinished work implementing stateless validation.
Serializer v4 amd laminas-i18n v3.0 are to be released.
The Release-candidate (RC) strategy proposal was discussed, but no firm decision was made.

Julian proposed creating AI/Claude skills and coding agent tooling, citing JetBrains stats that ~80% of PHP developers use some form of AI.
George dismissed it at first, though Tyrsson mentioned building an MCP for Mezzio and Rob was in favor of writing LLM skills to help AI agents correctly implement Laminas components.

The next TSC meeting was set for **Monday, October 5**.
