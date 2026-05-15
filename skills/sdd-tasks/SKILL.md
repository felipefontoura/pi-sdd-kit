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
   - Load relevant `.ai/steering/*.md` files when present, especially `product.md`, `tech-stack.md`, and `conventions.md`.

2. Locate the feature.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - Read `.status`.
   - Block if status is not `design:approved`, unless the user explicitly asks for draft planning.
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

5. Draft tasks.
   - Use the Tasks Template from `../_shared/references/templates.md`.
   - Include a Requirement Coverage table mapping requirements to task IDs.
   - Include stable task IDs, priority, estimate, dependencies, work checklist, acceptance criteria, files, and verification.
   - Ensure every Must Have requirement is covered by at least one task.
   - Include a dependency diagram only when it improves clarity.

6. Review with the user.
   - Present the full task breakdown.
   - Ask for explicit approval or requested changes.
   - Revise until approved.

7. Save draft and gate.
   - Save draft tasks to `.ai/sdd/specs/NNN-feature-name/tasks.md` with `> Status: Draft` when useful for collaboration.
   - Keep `.status` as `tasks:draft` until explicit approval.
   - After explicit approval, update the artifact status to approved and set `.status` to `tasks:approved`.

## Output

- `.ai/sdd/specs/NNN-feature-name/tasks.md`
- Updated `.status`

## Quality Bar

- Each task has acceptance criteria and verification.
- Each task has explicit dependencies.
- Each task names likely files.
- Every Must Have requirement is traceable to task IDs in the Requirement Coverage table.
- No task should be a vague bucket like "finish UI" or "fix bugs".

## Critical Rules

- Do not write implementation code in this skill.
- Do not invent technical details that conflict with `design.md`.
- If task planning reveals a design gap, stop and ask whether to update the design.
- Do not mark tasks approved without explicit user approval.
- Draft tasks may be saved, but they do not authorize implementation.
