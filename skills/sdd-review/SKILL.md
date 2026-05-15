---
name: sdd-review
description: 'Cognitive SDD skill for reviewing an implementation against requirements.md, design.md, and tasks.md, producing review.md with coverage, findings, verification evidence, and merge readiness. Use when the conversation calls for review after implementation or before completion, even without an explicit command. Do not use to implement fixes directly.'
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
   - Use the SDD Handoff Template and package-level `templates/handoff.md` when refreshing `.ai/sdd/handoff/sdd-brief.md` after review.
   - Load relevant `.ai/steering/*.md` files when present, especially conventions, principles, and verification rules.

2. Locate the feature and validate the gate.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - Read `.status`.
   - Validate `.status` against the official status values from `sdd-practical.md`.
   - If `.status` is missing or invalid, stop and ask the user to repair it; do not infer implementation completion from files or task checkboxes alone.
   - Prefer reviewing after `implementation:done`.
   - If status is `implementation:in-progress`, state that the review is partial and do not set `.status` to `review:done`.
   - If status is earlier than `implementation:in-progress`, block unless the user explicitly asks for a non-final artifact review.
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
   - Set `.status` to `review:done` only when starting from `implementation:done`, the review is complete, and the verdict is not blocked by missing information.
   - Do not advance `.status` for partial or non-final artifact reviews.
   - Update `.ai/sdd/INDEX.md` with the current status when practical; if not updated, tell the user the index may be stale.

8. Refresh the SDD handoff when review is complete.
   - If `.status` becomes `review:done`, update `.ai/sdd/handoff/sdd-brief.md` with review verdict, verification evidence summary, known follow-ups, blockers, and readiness for QA/release.
   - Preserve exact source paths to the reviewed spec artifacts.
   - Do not mark ready for release when verdict is `Needs fixes` or verification failed.

## Verdict Rules

- `Approved`: requirements pass, design is followed, verification passes, no blocking issues.
- `Approved with follow-ups`: core requirements pass, only low/medium non-blocking issues remain.
- `Needs fixes`: any Must Have requirement fails, verification fails, or high/critical issue exists.

## Output

- `.ai/sdd/specs/NNN-feature-name/review.md`
- Updated `.status` when complete
- Refreshed `.ai/sdd/handoff/sdd-brief.md` when `.status` becomes `review:done`

## Critical Rules

- Do not fix issues in this skill unless the user explicitly asks to switch to implementation.
- Do not mark review done if verification was skipped without explanation.
- Do not infer implementation completion from files or task checkboxes alone; require valid `.status`.
- Do not approve code that diverges from requirements, design, or traceability mappings unless the spec has been explicitly updated.
- Do not create noisy review reports; prioritize actionable findings.
- Do not use the handoff to hide review failures; blockers and failed verification must be explicit.
