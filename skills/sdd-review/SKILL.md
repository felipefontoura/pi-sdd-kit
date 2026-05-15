---
name: sdd-review
description: 'Reviews an SDD implementation against requirements.md, design.md, and tasks.md, producing review.md with requirement coverage, code quality findings, verification evidence, and merge readiness. Use after implementation or before completion. Do not use to implement fixes directly.'
---

# SDD Review

Validate implementation against the approved SDD artifacts.

## Purpose

Review checks whether the delivered code matches the product requirements, technical design, task plan, and project quality bar. It creates a concise but actionable `review.md` artifact.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when writing the review artifact.
   - Use package-level `templates/review.md` as the user-facing template when available.
   - Load relevant `.ai/steering/*.md` files when present, especially conventions and verification rules.

2. Locate the feature.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - Read `.status`.
   - Prefer reviewing after `implementation:done`.
   - If implementation is still in progress, state that the review is partial.
   - Read `requirements.md`, `design.md`, `tasks.md`, and `decisions.md` if present.

3. Identify review scope.
   - Use files listed in `tasks.md` as the starting scope.
   - Inspect current repository changes when available.
   - If scope is unclear, ask the user which files or feature area to review.

4. Review against the spec.
   - Check each functional requirement and acceptance criterion.
   - Check that design decisions and edge cases were implemented or intentionally updated.
   - Check task completion claims against actual code.
   - Flag missing, partial, or divergent behavior.

5. Review code quality.
   - Evaluate correctness, security, accessibility, performance, error/loading/empty states, maintainability, and tests.
   - Focus on high-signal findings.
   - Do not flag style issues already covered by formatters unless they indicate a larger problem.
   - Deduplicate repeated issues into one finding with affected files listed.

6. Verify.
   - Run project verification commands when available.
   - At minimum, run or identify lint/test/build equivalents for the stack.
   - If commands cannot run, document why and perform manual verification where possible.

7. Write review.
   - Use the Review Template from `../_shared/references/templates.md`.
   - Save as `.ai/sdd/specs/NNN-feature-name/review.md`.
   - Include coverage tables for requirements, tasks, and design decisions, plus quality check, verification result, issues found, and verdict.
   - Set `.status` to `review:done` only if the review is complete and the verdict is not blocked by missing information.

## Verdict Rules

- `Approved`: requirements pass, design is followed, verification passes, no blocking issues.
- `Approved with follow-ups`: core requirements pass, only low/medium non-blocking issues remain.
- `Needs fixes`: any Must Have requirement fails, verification fails, or high/critical issue exists.

## Critical Rules

- Do not fix issues in this skill unless the user explicitly asks to switch to implementation.
- Do not mark review done if verification was skipped without explanation.
- Do not approve code that diverges from requirements, design, or traceability mappings unless the spec has been explicitly updated.
- Do not create noisy review reports; prioritize actionable findings.
