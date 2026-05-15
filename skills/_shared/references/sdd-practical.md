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
    principles.md                  # optional project principles and decision rules
    *.md                           # optional domain docs, e.g. lp.md
  strategy/                        # optional upstream package output
    handoff/
      strategy-brief.md            # optional input to SDD when present
  sdd/
    INDEX.md                       # optional dashboard
    WORKFLOW.md                    # optional copy of the simple workflow guide
    PLAN.md                        # optional for small projects, recommended for medium
    handoff/
      sdd-brief.md                 # consolidated SDD output for downstream agents/packages
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
- `.ai/steering/principles.md` for project principles, `MUST`/`SHOULD`/`MAY` rules, decision rules, review expectations, and governance-like guidance.
- Additional `.ai/steering/*.md` files when the user or task domain indicates relevance.

Use `principles.md` for practical project rules rather than legalistic process. Prefer clear, testable principles that help users and agents make trade-offs.

Do not let steering override an approved feature artifact silently. If steering conflicts with requirements, design, or tasks, stop and ask which artifact should be updated.

## Upstream Handoff Input

SDD may consume optional handoff artifacts from upstream packages. The currently supported upstream handoff path is:

```text
.ai/strategy/handoff/strategy-brief.md
```

When present, treat this file as a compact strategic input for IDEA, PLAN, and PRD work. It may summarize market signal, user context, problem/outcome, product offer, unique mechanism, MVP scope, proof, messaging, acquisition path, risks, constraints, and readiness.

Rules:

- The strategy handoff is optional; SDD must work when it is missing.
- Read it when present and relevant, but do not require it.
- Use it to reduce rediscovery and seed SDD artifacts.
- Do not let it bypass SDD approval gates: requirements, design, and tasks still need explicit approval.
- If it conflicts with steering or existing approved SDD artifacts, stop and ask which source should be updated.

## SDD Handoff Output

SDD can produce a consolidated downstream handoff at:

```text
.ai/sdd/handoff/sdd-brief.md
```

This file is the SDD output contract for future agents, packages, or humans. It summarizes approved requirements, design decisions, tasks, verification expectations, review status, blockers, and readiness without replacing the source artifacts.

Rules:

- `sdd-brief.md` points to and summarizes `requirements.md`, `design.md`, `tasks.md`, `review.md`, `decisions.md`, and `.status`.
- Generate or refresh it after `tasks:approved` so downstream implementation packages can consume a stable implementation brief.
- Refresh it after `review:done` so QA, release, docs, or follow-up packages can consume review readiness.
- Do not use the handoff to silently change approved artifacts; update the source artifact first, then refresh the handoff.
- If multiple specs exist, the handoff may summarize the requested spec or the current release slice, but it must include exact source paths.

## Language Policy

The skill pack source, instructions, templates, headings, and reusable documentation are written in EN-US.

Runtime interaction is localized to the user's chat language:

- Detect the user's primary language from the message that started the current chat or skill request.
- Respond to the user in that language.
- Write generated project artifacts in that language, including `.ai/steering/`, `.ai/sdd/ideas/`, `.ai/sdd/PLAN.md`, `requirements.md`, `design.md`, `tasks.md`, `review.md`, and `.ai/sdd/handoff/sdd-brief.md`.
- Preserve technical identifiers, file names, status values, code symbols, commands, and stable IDs in their canonical form.
- If the user's language is ambiguous, default to EN-US and ask whether they prefer another language.
- Do not translate existing artifacts unless the user explicitly asks for translation or normalization.

## Feature Workspace Identity

Feature spec directories use this canonical form:

```text
.ai/sdd/specs/NNN-feature-slug/
```

When creating a new feature spec directory, do not guess the number from memory or from `.ai/sdd/INDEX.md`. Determine it from the filesystem every time:

1. List actual directories under `.ai/sdd/specs/`.
2. Consider only directory names that start with one or more digits followed by `-`, matching `^([0-9]+)-`.
3. Extract the numeric prefixes as integers.
4. If no matching directories exist, use `001`.
5. Otherwise use `max(existing numeric prefixes) + 1`.
6. Zero-pad to at least 3 digits. If existing prefixes use a wider width, preserve the widest existing width.
7. Never reuse a numeric prefix, even if a directory looks abandoned, unless the user explicitly instructs a cleanup/rename.
8. Before creating files, state the resolved path and ask for confirmation if there is any ambiguity.

Slug rules:

- Use 2-5 meaningful words from the feature name.
- Use lowercase ASCII when practical.
- Replace spaces and separators with `-`.
- Remove punctuation and unsafe filesystem characters.
- Collapse repeated hyphens and trim leading/trailing hyphens.
- Preserve common technical tokens when readable, such as `api`, `oauth2`, `sso`, `jwt`.
- If a safe slug cannot be derived confidently, ask the user for a short slug.

Existing feature resolution:

- If the user names an existing feature, match against actual spec directories and artifact titles.
- If exactly one match is found, use it.
- If multiple plausible matches exist, list the candidates and ask the user to choose.
- Do not create a new spec when the user likely meant to update an existing one.

Index policy:

- `.ai/sdd/INDEX.md` is a dashboard, not the source of truth for numbering.
- Use the filesystem and `.status` files as source of truth.
- If a skill already writes a primary artifact (`requirements.md`, `design.md`, `tasks.md`, `review.md`, or `.status`), it should also update the relevant `INDEX.md` row in the same operation when practical.
- If the skill does not update `INDEX.md`, it must explicitly report that the index may be stale.

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

## Status Validation and Gate Hardening

`.status` is the source of truth for SDD gate state. File existence does not imply approval.

Before any skill relies on or changes a feature status:

1. Read `.ai/sdd/specs/NNN-feature-name/.status`.
2. Verify the value exactly matches one of the valid status values above.
3. If `.status` is missing, stop and ask the user whether to create or repair it; do not infer approval from artifacts.
4. If `.status` is invalid, stop, show the invalid value, list valid values, and ask which correction to apply.
5. If the requested skill is not allowed by the current status, block and recommend the next safe command.
6. When changing status, update `.status`, update the artifact header status when applicable, and update `.ai/sdd/INDEX.md` when practical.
7. If `.status` conflicts with artifact headers or obvious artifact state, stop and ask which source should be corrected.

Allowed normal transitions:

```text
requirements:draft -> requirements:approved
requirements:approved -> design:draft

design:draft -> design:approved
design:approved -> tasks:draft

tasks:draft -> tasks:approved
tasks:approved -> implementation:in-progress
implementation:in-progress -> implementation:done
implementation:done -> review:done
```

Permitted draft/spike exceptions:

- `design.md` may be created as a non-binding draft spike before `requirements:approved` only when explicitly requested by the user; keep `.status` at the current gate unless the user approves the proper transition.
- `tasks.md` may be created as draft planning before `design:approved` only when explicitly requested by the user; keep `.status` at the current gate unless the user approves the proper transition.
- Implementation spikes before `tasks:approved` are outside the approved SDD flow; label them clearly as spikes and do not mark SDD tasks complete.

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
- `.ai/sdd/handoff/sdd-brief.md` maps downstream readiness back to source requirements, design, tasks, and review artifacts.
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

Clarification is part of PRD work, not a separate required workflow phase. When requirement ambiguity exists, help the user decide with guided choices rather than broad open-ended questions:

- ask one question at a time;
- explain why the answer matters;
- recommend the safest or simplest default when appropriate;
- provide 2-4 concrete options plus `Custom` when useful;
- describe the practical impact of each option;
- ask only questions that materially change scope, UX, security/privacy, data behavior, acceptance criteria, or important NFRs;
- avoid technical implementation questions that belong in design.

Use these sections in `requirements.md`:

- `Questions`: unresolved or answered requirement questions, identified as `Q-001`, `Q-002`, ... with status `open` or `answered`.
- `Decisions`: resolved product or requirement choices, identified as `D-001`, `D-002`, ... with reason, source question when applicable, and impacted requirement IDs or sections.

Open critical questions may remain in a draft, but they block `requirements:approved`. When a question is answered, update the affected user stories, requirements, NFRs, or scope boundaries; do not only record the answer in `Questions`.

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

`TASKS` includes the implementation readiness check. Do not add a separate public analysis phase unless explicitly requested. Before approving tasks, verify:

- requirements are covered by design decisions or design sections;
- every Must Have requirement has at least one task;
- every task maps to a requirement, NFR, design decision, or explicit enabling need;
- critical `Questions` in `requirements.md` are answered;
- each task has dependencies, acceptance criteria, likely files, and verification;
- verification commands are known or explicitly marked manual/N/A.

When user stories exist, group work into lightweight implementation slices when helpful:

- MVP slice;
- `US-001`, `US-002`, ... slices;
- polish or cross-cutting work.

Keep slices optional for small features. Prefer clarity over ceremony.

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
