---
status: pending
title: [Task title]
type: [frontend|backend|docs|test|infra|refactor|chore|bugfix]
complexity: [low|medium|high|critical]
dependencies: []
---

# Task [N]: [Title]

## Overview

[2-3 sentences: what the task accomplishes and why it matters.]

## Context

- Requirements: @requirements.md
- Design: @design.md
- Covers: FR-001, NFR-001

## Requirements

- [Requirement this task must satisfy]
- [Requirement this task must satisfy]

## Subtasks

- [ ] [Subtask — WHAT to accomplish]
- [ ] [Subtask — WHAT to accomplish]

## Implementation Details

[File paths, integration points, and relevant dependencies. Reference `design.md` for patterns and contracts instead of duplicating the full technical design.]

### Relevant Files

- `path/to/file` — [why this file is relevant]

### Dependent Files

- `path/to/dependency` — [why this file is affected]

### Related Decisions

- TD-001 — [Relevance]
- ADR-001 — [Relevance]

## Deliverables

- [Concrete output]
- [Tests updated or added]
- [Documentation/config updated if needed]

## Tests

- Unit/component:
  - [ ] [Test case]
- Integration/API:
  - [ ] [Test case]
- Manual:
  - [ ] [Scenario]

## Success Criteria

- [ ] Acceptance criteria satisfied
- [ ] Relevant tests pass
- [ ] Lint/typecheck/build pass as appropriate
- [ ] No unrelated scope added

## Verification Evidence

```text
Command: [exact command or manual check]
Exit code: [0/non-zero/not applicable]
Summary: [what passed/failed]
Verdict: PASS/FAIL
```
