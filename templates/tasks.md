# Tasks: [Feature]

> Requirements: @requirements.md
> Design: @design.md
> Status: Draft
> Last Updated: YYYY-MM-DD

## Requirement Coverage

| Requirement | Tasks | Notes |
|-------------|-------|-------|
| FR-001 | T1, T2 | |
| NFR-001 | T3 | |

## Design Coverage Check

| Requirement | Design Coverage | Status | Notes |
|-------------|-----------------|--------|-------|
| FR-001 | design.md section / TD-001 | Pass/Fail/Partial | |
| NFR-001 | design.md section / TD-002 | Pass/Fail/Partial | |

## Implementation Readiness Check

| Check | Status | Notes |
|-------|--------|-------|
| Must Have requirements have tasks | Pass/Fail | |
| Tasks map to requirements, NFRs, design decisions, or enabling work | Pass/Fail | |
| Critical Questions in requirements.md are answered | Pass/Fail/N/A | |
| Tasks have dependencies, acceptance criteria, files, and verification | Pass/Fail | |
| Verification commands are identified or marked manual/N/A | Pass/Fail | |
| No blocking design or requirements gaps remain | Pass/Fail | |

> Do not approve tasks while any readiness check has blocking `Fail` status.

## Implementation Slices

Use this section when user-story or MVP slices improve clarity. Keep it short for small features.

### MVP Slice

- **Goal:** [Smallest valuable increment]
- **User Stories:** US-001
- **Tasks:** T1, T2
- **Independent validation:** [How this slice can be verified]

### US-001 Slice: [Title]

- **Goal:** [What this user story delivers]
- **Tasks:** T1, T2
- **Independent validation:** [How to verify this story without unrelated stories]

### Polish / Cross-Cutting

- **Tasks:** [T...] 
- **Purpose:** [Cleanup, docs, performance, accessibility, security, or release readiness]

## Task Summary

| Task | Title | Priority | Estimate | Dependencies | Status |
|------|-------|----------|----------|--------------|--------|
| T1 | [Title] | P0 | 1h | none | pending |
| T2 | [Title] | P1 | 2h | T1 | pending |

## Dependency Diagram

```mermaid
flowchart LR
    T1[T1: First task] --> T2[T2: Second task]
```

## Task T1: [Title]

**Priority:** P0  
**Estimate:** [30m / 1h / 2h / 4h]  
**Dependencies:** none  
**Covers:** FR-001, NFR-001  
**Status:** pending

### Overview

[2-3 sentences: what this task accomplishes and why it matters.]

### Work

- [ ] [Subtask — WHAT to accomplish]
- [ ] [Subtask — WHAT to accomplish]

### Acceptance Criteria

- [ ] [Verifiable result]
- [ ] [Verifiable result]

### Files

- `path/to/file.tsx` — create/modify; [why]
- `path/to/test.tsx` — create/modify; [why]

### Verification

- [ ] Unit/component tests pass: `[command]`
- [ ] Integration/API tests pass: `[command or N/A]`
- [ ] Lint/typecheck passes: `[command]`
- [ ] Build passes: `[command]`
- [ ] Manual behavior checked: [scenario]

### Notes

- Reference `design.md` for implementation details. Do not duplicate design decisions here.

## Task T2: [Title]

**Priority:** P1  
**Estimate:** [30m / 1h / 2h / 4h]  
**Dependencies:** T1  
**Covers:** FR-002  
**Status:** pending

### Overview

[2-3 sentences.]

### Work

- [ ] [Subtask]

### Acceptance Criteria

- [ ] [Verifiable result]

### Files

- `path/to/file` — create/modify; [why]

### Verification

- [ ] [Verification]

## Completion Rules

- Do not mark a task complete without implementation and verification evidence.
- Do not create separate testing-only tasks unless the project is about test infrastructure.
- Tests and verification belong inside each implementation task.
- If a task reveals a requirements or design gap, stop and update the relevant artifact through the proper gate.
