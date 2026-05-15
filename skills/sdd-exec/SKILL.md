---
name: sdd-exec
description: 'Implements approved SDD tasks from tasks.md with tight scope, repository conventions, tests, and verification evidence. Use when the user asks to execute a specific SDD task or implement an approved feature. Do not use before tasks are approved.'
---

# SDD Exec

Implement approved tasks while preserving traceability to requirements and design.

## Purpose

Execution turns approved specs into code. The agent must stay within the task scope, follow project conventions, verify the result, and update task status only when evidence exists.

## Workflow

1. Load the SDD reference.
   - Read `../_shared/references/sdd-practical.md`.
   - Apply the Language Policy: respond and write artifacts in the user's initial chat language while keeping skill instructions and templates in EN-US.
   - Load relevant `.ai/steering/*.md` files when present, especially `tech-stack.md`, `conventions.md`, and `principles.md`.

2. Locate the feature and task, then validate the gate.
   - Use `.ai/sdd/specs/NNN-feature-name/`.
   - Read `.status`.
   - Validate `.status` against the official status values from `sdd-practical.md`.
   - If `.status` is missing or invalid, stop and ask the user to repair it; do not infer task approval from `tasks.md` existing.
   - Block if status is not `tasks:approved` or `implementation:in-progress`, unless the user explicitly requests a spike.
   - If blocked, report the current status and recommend `/skill:sdd-tasks` approval as the next safe action.
   - Read `requirements.md`, `design.md`, `tasks.md`, and `decisions.md` if present.
   - Identify the requested task. If no task is specified, select the first incomplete task whose dependencies are complete and confirm with the user.

3. Reconcile workspace state.
   - Inspect current files before editing.
   - Do not overwrite user changes.
   - If unexpected edits overlap with the task, stop and ask how to proceed.

4. Build an execution checklist.
   - Extract task work items, acceptance criteria, file targets, and verification items.
   - Print the checklist before editing.
   - Set `.status` to `implementation:in-progress` when starting implementation from `tasks:approved`.
   - If already `implementation:in-progress`, preserve that status while continuing incomplete approved tasks.

5. Implement.
   - Keep scope limited to the selected task.
   - Follow existing project patterns and real dependency APIs.
   - Add or update tests when behavior changes or regressions are possible.
   - Stop if requirements and design conflict; do not guess.
   - Record any necessary spec change as a proposed update, not an implicit code divergence.

6. Verify.
   - Run task-specific verification first when listed.
   - Run the broad project verification command when available: lint, test, build, or the project-defined gate.
   - If no automated verification exists, perform manual checks and state the limitation.
   - Do not claim completion without fresh verification evidence.

7. Update tracking.
   - Mark completed checklist items in `tasks.md` only after evidence exists.
   - Mark the task complete only after implementation and verification pass.
   - If all tasks are complete, set `.status` to `implementation:done`.
   - Otherwise keep `.status` as `implementation:in-progress`.
   - Update `.ai/sdd/INDEX.md` with the current status when practical; if not updated, tell the user the index may be stale.

8. Report.
   - Summarize files changed.
   - Summarize requirements/design coverage.
   - Include verification report with exact command, exit code, summary, and PASS/FAIL verdict.
   - Suggest the next incomplete task or recommend review when all tasks are complete.

## Verification Report Format

```text
VERIFICATION REPORT
Claim: [claim]
Command: [exact command or manual check]
Exit code: [0/non-zero/not applicable]
Output summary: [key result]
Errors: [none or summary]
Verdict: PASS/FAIL
```

## Critical Rules

- Do not implement before `tasks:approved`.
- Do not infer task approval from file existence; require valid `.status`.
- Do not expand scope beyond the selected task.
- Do not mark work complete without verification evidence.
- Do not hide failing checks; report actual status.
- Do not update requirements or design silently during implementation.
