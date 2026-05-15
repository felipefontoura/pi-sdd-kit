---
name: sdd-tasks
description: 'Decomposes an approved SDD design.md into practical tasks.md for small and medium projects. Use for implementation planning, task dependencies, estimates, acceptance criteria, file targets, and verification steps. Do not use for technical design or direct coding.'
---

# SDD Tasks

Convert an approved design into an implementation task plan.

## Purpose

Tasks define how much work exists and in what order it should be done. They must be small, independently implementable, dependency-aware, and verifiable.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Read `../_shared/references/templates.md` when drafting the artifact.
   - Use package-level `templates/tasks.md` as the user-facing template when available.
   - Use the SDD Handoff Template and package-level `templates/handoff.md` when creating or refreshing `.ai/sdd/handoff/sdd-brief.md`.
   - Load relevant `.ai/steering/*.md` files when present, especially `product.md`, `tech-stack.md`, `conventions.md`, and `principles.md`.

2. Locate the feature and validate the gate.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - Read `.status`.
   - Validate `.status` against the official status values from `sdd-practical.md`.
   - If `.status` is missing or invalid, stop and ask the user to repair it; do not infer design approval from `design.md` existing.
   - Block if status is not `design:approved`, unless the user explicitly asks for draft planning.
   - If blocked, report the current status and recommend `/skill:sdd-spec` approval as the next safe action.
   - Read `requirements.md` and `design.md` completely.
   - Read `decisions.md` if it exists.

3. Explore implementation context.
   - Inspect relevant files, tests, package scripts, project conventions, and existing patterns.
   - Identify likely files to create or modify.
   - Identify verification commands from `package.json`, Makefile, README, CI config, or project docs.

4. Decompose work.
   - Create tasks that are independently implementable after dependencies are complete.
   - Avoid circular dependencies.
   - Keep small-project tasks around 30 minutes to 2 hours.
   - Keep medium-project tasks around 1 to 4 hours.
   - Merge tasks that cannot be verified independently.
   - Include tests and verification inside each task; do not create a separate testing-only task unless explicitly needed.
   - Prefer implementation slices that deliver visible value when the requirements contain user stories.
   - For small projects, keep slices lightweight and optional; do not add ceremony when a flat task list is clearer.

5. Run the implementation readiness check.
   - Keep this as part of `sdd-tasks`; do not introduce a separate public analysis step.
   - Verify requirements are covered by design decisions or design sections.
   - Verify every Must Have requirement is covered by at least one task.
   - Verify every task maps to at least one requirement, NFR, design decision, or explicit enabling need.
   - Verify critical `Questions` in `requirements.md` are answered before approval.
   - Verify each task has acceptance criteria, likely files, dependencies, and verification.
   - Verify planned verification commands are known or explicitly marked manual/N/A.
   - If the check reveals a requirements or design gap, stop and ask whether to update the source artifact before continuing.

6. Draft tasks.
   - Use the Tasks Template from `../_shared/references/templates.md`.
   - Include a Requirement Coverage table mapping requirements to task IDs.
   - Include a Readiness Check table summarizing coverage, open questions, task quality, and verification readiness.
   - Include optional Implementation Slices for MVP / user stories when they improve clarity.
   - Include stable task IDs, priority, estimate, dependencies, work checklist, acceptance criteria, files, and verification.
   - Ensure every Must Have requirement is covered by at least one task.
   - Include a dependency diagram only when it improves clarity.

7. Review with the user.
   - Present the full task breakdown.
   - Ask for explicit approval or requested changes.
   - Revise until approved.

8. Save draft and gate.
   - Save draft tasks to `.ai/sdd/specs/NNN-feature-name/tasks.md` with `> Status: Draft` when useful for collaboration.
   - Set `.status` to `tasks:draft` only after a binding task draft is created from `design:approved`.
   - For draft planning before approved design, do not advance `.status`; clearly label the draft as non-binding.
   - Keep `.status` as `tasks:draft` until explicit approval.
   - Do not mark tasks approved while the Readiness Check has blocking failures.
   - After explicit approval, update the artifact status header to approved and set `.status` to `tasks:approved`.
   - Update `.ai/sdd/INDEX.md` with the current status when practical; if not updated, tell the user the index may be stale.

9. Create or refresh the SDD handoff after approval.
   - Only after `tasks:approved`, create `.ai/sdd/handoff/` if needed.
   - Write or update `.ai/sdd/handoff/sdd-brief.md` as the downstream implementation contract.
   - Summarize the approved requirements, design, task order, likely files, verification plan, blockers, and readiness.
   - Include exact source paths to `requirements.md`, `design.md`, `tasks.md`, `.status`, optional `decisions.md`, and optional `.ai/strategy/handoff/strategy-brief.md` if it was used.
   - Mark readiness as ready for implementation only when requirements, design, and tasks are approved and no blocking open questions remain.

## Output

- `.ai/sdd/specs/NNN-feature-name/tasks.md`
- Updated `.status`
- `.ai/sdd/handoff/sdd-brief.md` after `tasks:approved`

## Quality Bar

- Each task has acceptance criteria and verification.
- Each task has explicit dependencies.
- Each task names likely files.
- Every Must Have requirement is traceable to task IDs in the Requirement Coverage table.
- Readiness Check has no blocking failures before approval.
- Open critical requirement questions are resolved before approval.
- No task should be a vague bucket like "finish UI" or "fix bugs".

## Critical Rules

- Do not write implementation code in this skill.
- Do not invent technical details that conflict with `design.md`.
- If task planning reveals a design gap, stop and ask whether to update the design.
- Do not mark tasks approved without explicit user approval.
- Draft tasks may be saved, but they do not authorize implementation.
- Do not write `.ai/sdd/handoff/sdd-brief.md` as ready for implementation before `tasks:approved`.
- Do not infer design approval from file existence; require valid `.status`.
