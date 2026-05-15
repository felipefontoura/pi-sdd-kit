# SDD Practical Reference

A lightweight but rigorous Spec-Driven Development workflow for small and medium projects.

## Core Pipeline

```text
IDEA -> PLAN -> REQUIREMENTS -> DESIGN -> TASKS -> IMPLEMENTATION -> REVIEW
```

- `IDEA`: divergent exploration before planning. No commitment yet.
- `PLAN`: optional for small work, recommended for medium projects. Maps roadmap and feature boundaries.
- `REQUIREMENTS`: business/product contract. Defines WHAT and WHY.
- `DESIGN`: technical contract. Defines HOW and trade-offs.
- `TASKS`: implementation plan. Defines HOW MUCH work and dependencies.
- `IMPLEMENTATION`: code execution against approved specs.
- `REVIEW`: verifies implementation against requirements, design, and tasks.

## Recommended Directory Structure

```text
.ai/
  steering/                        # reusable project context for any AI workflow
    product.md                     # product vision, users, goals, constraints
    tech-stack.md                  # frameworks, libraries, versions, infrastructure
    conventions.md                 # code style, architecture, naming, workflow rules
    *.md                           # optional domain docs, e.g. lp.md
  sdd/
    INDEX.md                       # optional dashboard
    PLAN.md                        # optional for small projects, recommended for medium
    ideas/
      001-feature-idea.md
    specs/
      001-feature-name/
        .status
        requirements.md
        design.md
        tasks.md
        review.md
        decisions.md               # optional lightweight ADR log
```

## Steering Context

Steering documents are persistent project guidance shared across SDD and non-SDD skills.

When present, read only the steering files relevant to the requested work:

- `.ai/steering/product.md` for product vision, personas, value proposition, scope boundaries, and success metrics.
- `.ai/steering/tech-stack.md` for stack, versions, architectural constraints, infrastructure, and approved dependencies.
- `.ai/steering/conventions.md` for coding standards, naming, folder patterns, test strategy, accessibility/security rules, and team workflow.
- Additional `.ai/steering/*.md` files when the user or task domain indicates relevance.

Do not let steering override an approved feature artifact silently. If steering conflicts with requirements, design, or tasks, stop and ask which artifact should be updated.

## Language Policy

The skill pack source, instructions, templates, headings, and reusable documentation are written in EN-US.

Runtime interaction is localized to the user's chat language:

- Detect the user's primary language from the message that started the current chat or skill request.
- Respond to the user in that language.
- Write generated project artifacts in that language, including `.ai/steering/`, `.ai/sdd/ideas/`, `.ai/sdd/PLAN.md`, `requirements.md`, `design.md`, `tasks.md`, and `review.md`.
- Preserve technical identifiers, file names, status values, code symbols, commands, and stable IDs in their canonical form.
- If the user's language is ambiguous, default to EN-US and ask whether they prefer another language.
- Do not translate existing artifacts unless the user explicitly asks for translation or normalization.

## Status Values

Each feature spec directory MUST have a `.status` file with one of:

```text
idea:exploring
idea:captured
plan:draft
plan:approved
requirements:draft
requirements:approved
design:draft
design:approved
tasks:draft
tasks:approved
implementation:in-progress
implementation:done
review:done
```

## Draft and Approval Policy

Draft artifacts may be saved before approval so work is not lost and collaboration remains visible.

- Saving a draft is allowed for `PLAN.md`, `requirements.md`, `design.md`, and `tasks.md`.
- Draft files MUST keep their draft status in the document header and `.status`.
- Draft artifacts MUST NOT unlock the next gate.
- Only explicit human approval may promote a draft to `*:approved`.
- When promoting to approved, update both the artifact status header and `.status`.
- If a later phase reveals a gap in an approved artifact, propose an update and ask for approval before proceeding.

## Gate Rules

- Do not write code before `tasks:approved`.
- Do not create a binding `design.md` before `requirements.md` is approved, unless the user explicitly asks for a non-binding draft spike.
- Do not create a binding `tasks.md` before `design.md` is approved, unless the user explicitly asks for draft planning.
- Do not claim implementation complete without fresh verification evidence.
- If ambiguity appears during implementation, stop and ask whether to update the relevant spec.

## Traceability Rules

Use stable IDs so the AI and humans can maintain artifacts safely:

- User stories: `US-001`, `US-002`
- Functional requirements: `FR-001`, `FR-002`
- Non-functional requirements: `NFR-001`, `NFR-002`
- Technical decisions: `TD-001`, `TD-002`
- Tasks: `T1`, `T2` or `T1.1`, `T1.2`

Traceability should be lightweight:

- `design.md` maps requirements to design sections or decisions.
- `tasks.md` maps requirements to implementation tasks.
- `review.md` maps requirements and tasks to pass/fail evidence.
- Update mappings only when requirements, design, or tasks change.
- Keep tables concise; do not create exhaustive bureaucracy for trivial features.

## Small vs Medium Project Rules

### Small project

Examples: landing page, one UI flow, small dashboard, isolated frontend feature.

- `PLAN.md` is optional.
- Use one spec directory per feature or screen.
- Keep tasks between 30 minutes and 2 hours.
- Keep design concise: components, state/data, flows, edge cases, decisions.
- Use rich template sections only when relevant; mark irrelevant sections as `Not applicable` or omit them if the artifact remains clear.

### Medium project

Examples: small SaaS, admin panel, app with auth, multi-module frontend/backend.

- `PLAN.md` is recommended before feature specs.
- Use one spec directory per major feature.
- Keep tasks between 1 and 4 hours.
- Track technical decisions in `decisions.md` when trade-offs matter.
- Include data model, API/integration contracts, security/permissions, observability, migration, rollout, and operational risks when relevant.

## Requirements Writing

Use business/product language. Requirements answer WHAT and WHY, not implementation details.

Prefer EARS style for functional requirements:

```text
WHEN [event]
IF [condition]
THE SYSTEM SHALL [behavior]
SO THAT [outcome]
```

Use MoSCoW priority:

- Must Have: required for the feature to work.
- Should Have: important but has a workaround.
- Could Have: desirable if cheap.
- Won't Have: explicitly out of scope for this version.

## Design Writing

Design answers HOW. Include only the technical detail needed to implement correctly:

- requirements mapping
- chosen approach and trade-offs
- component/module structure
- data model and state ownership
- API/integration boundaries if applicable
- security, permissions, privacy, and accessibility where relevant
- edge cases
- verification strategy
- risks and mitigations
- rollout/migration/observability where relevant
- implementation FAQ

## Task Writing

Tasks must be independently implementable once dependencies are complete.

Each task should include:

- stable task ID
- requirement coverage
- priority
- estimate
- dependencies
- work checklist
- acceptance criteria
- files likely created/modified
- verification checklist

Do not create separate testing-only tasks unless the project is explicitly about test infrastructure. Tests belong inside each implementation task.

## Verification

Match verification scope to the claim:

- Narrow claim: run the specific relevant test/check.
- Completion claim: run the full project verification command when available, usually lint + test + build.
- If no command exists, perform manual verification and state the limitation.

Always report:

```text
Command: <exact command or manual check>
Exit code: <0/non-zero/not applicable>
Summary: <what passed/failed>
Verdict: PASS or FAIL
```
