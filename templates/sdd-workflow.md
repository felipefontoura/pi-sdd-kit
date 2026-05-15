# SDD Workflow Guide

> Purpose: Help humans and AI agents follow the SDD flow without adding extra process ceremony.
> Last Updated: YYYY-MM-DD

## Simple Flow

```text
IDEA → PLAN → PRD → SPEC → TASKS → EXEC → REVIEW
```

The flow is intentionally simple. Most quality checks are built into the existing steps instead of becoming separate commands.

## Step-by-Step

### 1. IDEA

Use when the direction is still unclear.

**Command:** `/skill:sdd-idea`

**Use this to:**

- explore a raw idea;
- compare possible directions;
- identify users, value, risks, and constraints;
- decide whether to continue, plan, or create requirements directly.

**Typical output:** `.ai/sdd/ideas/001-feature-idea.md`

### 2. PLAN

Use when there are multiple features, phases, personas, or dependencies.

**Command:** `/skill:sdd-plan`

**Use this to:**

- define MVP boundaries;
- organize features into phases;
- map dependencies;
- align the roadmap before writing feature requirements.

**Typical output:** `.ai/sdd/PLAN.md`

**Small feature shortcut:** skip PLAN and go directly to PRD.

### 3. PRD

Use to define WHAT and WHY.

**Command:** `/skill:sdd-prd`

**Use this to:**

- define users and business context;
- write user stories and acceptance criteria;
- write functional and non-functional requirements;
- define out-of-scope boundaries;
- resolve important requirement ambiguity.

PRD includes built-in clarification:

- `Questions` capture open or answered requirement questions.
- `Decisions` capture resolved product or requirement choices.

A question should become a decision when answered, and the affected requirements should be updated.

**Typical output:** `.ai/sdd/specs/NNN-feature-name/requirements.md`

**Gate:** requirements must be explicitly approved before binding SPEC work.

### 4. SPEC

Use to define HOW.

**Command:** `/skill:sdd-spec`

**Use this to:**

- map requirements to technical design;
- define architecture, components, data/state, APIs, integrations, and edge cases;
- document technical decisions and trade-offs;
- define verification strategy.

**Typical output:** `.ai/sdd/specs/NNN-feature-name/design.md`

**Gate:** design must be explicitly approved before binding TASKS work.

### 5. TASKS

Use to define implementation work and readiness.

**Command:** `/skill:sdd-tasks`

**Use this to:**

- break approved design into small tasks;
- map requirements to tasks;
- define dependencies, files, acceptance criteria, and verification;
- check whether implementation is ready to start.

TASKS includes built-in readiness checks:

- requirements are covered by design;
- Must Have requirements have tasks;
- tasks map to requirements, NFRs, design decisions, or enabling work;
- critical PRD questions are answered;
- tasks include dependencies, files, acceptance criteria, and verification.

TASKS may also include lightweight implementation slices:

- MVP Slice;
- `US-001`, `US-002`, ... slices;
- Polish / Cross-Cutting.

**Typical output:** `.ai/sdd/specs/NNN-feature-name/tasks.md`

**Gate:** tasks must be explicitly approved before EXEC.

### 6. EXEC

Use to implement approved tasks.

**Command:** `/skill:sdd-exec`

**Use this to:**

- execute one approved task at a time;
- keep scope limited;
- update tests or verification;
- record fresh verification evidence;
- update task progress only after evidence exists.

**Allowed status:** `tasks:approved` or `implementation:in-progress`

**Typical result:** code changes, updated `tasks.md`, updated `.status`.

### 7. REVIEW

Use after implementation to verify the result.

**Command:** `/skill:sdd-review`

**Use this to:**

- compare implementation against requirements, design, and tasks;
- check coverage and quality;
- run or record verification;
- identify blockers or follow-ups;
- determine merge/readiness verdict.

**Typical output:** `.ai/sdd/specs/NNN-feature-name/review.md`

## Small Feature Shortcut

For small isolated work, use:

```text
PRD → SPEC → TASKS → EXEC → REVIEW
```

Use IDEA only if the idea is unclear. Use PLAN only if there are multiple features, phases, or dependencies.

## Steering Context

Reusable project context lives in:

```text
.ai/steering/
```

Common files:

- `product.md` — product vision, users, value, boundaries;
- `tech-stack.md` — runtime, frameworks, infrastructure, verification commands;
- `conventions.md` — code style, architecture patterns, testing, workflow;
- `principles.md` — project principles, `MUST`/`SHOULD`/`MAY` rules, decision rules, review expectations.

Use `/skill:sdd-steering` to create or update these files.

## Gates and Status

Each feature spec has a `.status` file.

```text
requirements:draft → requirements:approved
design:draft → design:approved
tasks:draft → tasks:approved
tasks:approved → implementation:in-progress
implementation:in-progress → implementation:done
implementation:done → review:done
```

Rules:

- Drafts may be saved, but drafts do not unlock the next phase.
- File existence does not mean approval.
- `.status` is the source of truth for gates.
- Skills should stop when `.status` is missing, invalid, or inconsistent.
- Human approval is required for requirements, design, and tasks approval.

## Feature IDs

Feature directories use:

```text
.ai/sdd/specs/NNN-feature-slug/
```

Numbering source is the filesystem, not `INDEX.md`.

When creating a new feature:

1. list directories under `.ai/sdd/specs/`;
2. extract numeric prefixes from names like `001-feature`;
3. use `max + 1`;
4. zero-pad to at least 3 digits;
5. create a short, safe slug.

## Recommended Next Action

If unsure where to start:

- unclear idea → `/skill:sdd-idea`;
- multiple features → `/skill:sdd-plan`;
- known feature → `/skill:sdd-prd`;
- approved requirements → `/skill:sdd-spec`;
- approved design → `/skill:sdd-tasks`;
- approved tasks → `/skill:sdd-exec`;
- implemented feature → `/skill:sdd-review`;
- unsure current state → `/skill:sdd-status`.
