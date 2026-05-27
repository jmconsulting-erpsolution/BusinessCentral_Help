# Documentation Index

This folder contains project documentation for the JM Connector-4-Rivelio extension.

## Core Documentation

- **[TECHNICAL_DOCUMENTATION.md](TECHNICAL_DOCUMENTATION.md)** — Architecture, AL objects, data model, integrations, deployment notes, and technical debt tracking.
- **[FUNCTIONAL_DOCUMENTATION.md](FUNCTIONAL_DOCUMENTATION.md)** — Business goals, scope, user flows, validation rules, acceptance criteria, and known limitations.
- **[changelog.md](changelog.md)** — Project change history (reverse chronological, newest first).

## Workflows (in `.github/prompts/`)

Prompts for common tasks reference the skills in `.github/skills/`:

- `/generate-documentation` — Execute the docs-update skill to keep `/.docs` synchronized after each coding task.
- `/tdd` — Test-driven development workflow for AL code.
- `/fix-cops` — Fix AL compilation errors.
- Other prompts: `/create-api`, `/extract-interface`, `/translate-it-it-xlf`, `/verify-coverage`, `/verify-wrapper`, `/verify-mock`.

## Skills (in `.github/skills/`)

- `docs-update` — 8-step workflow to keep documentation in sync (run at end of every coding task).
- `tdd` — Test-driven development for AL.
- `writing-al-code` — AL coding conventions and best practices.
- `writing-unit-tests` — AL unit test patterns.
- `writing-mocks` — Creating mock codeunits for interfaces.
- `using-mocks` — Consuming existing mocks in tests.
- `writing-wrappers` — Wrapping external code.
- `adding-number-series` — Implementing No. Series sequencing.

## Mandatory AL Data-Access Rule

- Before reading any table `FlowField` or `BLOB` field, call `CalcFields(...)` for that field.
- If `FlowField` values are read inside a loop, call `SetAutoCalcFields(...)` before `FindSet/FindFirst/FindLast/Find` and before entering the loop.
- Include all read `FlowField` fields in `CalcFields(...)`/`SetAutoCalcFields(...)`.
- Preferred loop pattern:
	- `Customer.SetAutoCalcFields(Balance, "Net Change");`
	- `if Customer.FindSet() then repeat ... until Customer.Next() = 0;`

Reference: `.github/instructions/calcfields-before-reading.instructions.md`.

---

**Last updated**: 2026-05-27
