# Pi SDD Kit

A skill pack for the [Pi Coding Agent](https://www.npmjs.com/package/@earendil-works/pi-coding-agent) that implements a practical **Specification-Driven Development (SDD)** workflow for small and medium projects.

It helps turn raw ideas into implemented software through explicit artifacts, human gates, validated status transitions, traceability, and verification.

```text
IDEA → PLAN → PRD → SPEC → TASKS → EXEC → REVIEW
```

The pack also includes skills to initialize the AI workspace, maintain reusable project context, inspect the current SDD status, consume optional upstream handoffs, produce downstream handoff briefs, and provide ready-to-use templates for users.

> **The spec is the contract. Code is a consequence of it.** This kit turns that principle into an enforceable workflow — explicit artifacts, human approval gates, and a `.status` file that is the single source of truth for what is approved.

Built by [Felipe Fontoura](https://felipefontoura.com), who used Spec-Driven Development to ship a [13-app crypto fintech solo in 70 days](https://felipefontoura.com/articles/spec-driven-development-case-study). New to the methodology? Start with the complete guide: [**What Is Spec-Driven Development?**](https://felipefontoura.com/articles/what-is-spec-driven-development)

---

## Language policy

This package source, skill instructions, templates, and documentation are written in **EN-US**.

At runtime, skills should adapt to the user's chat language:

- respond in the language used by the user at the start of the chat or skill request;
- write generated project artifacts in that same language;
- preserve canonical technical identifiers such as file names, status values, commands, code symbols, and stable IDs;
- default to EN-US when the user's language is ambiguous.

Example: if the user starts in Portuguese, the skill should answer in Portuguese and write `requirements.md`, `design.md`, `tasks.md`, etc. in Portuguese, while keeping paths, status values, and IDs unchanged.

---

## Additional study material

For a deeper explanation of the SDD methodology and examples of how to use the workflow, see:

- [What Is Spec-Driven Development? A Practitioner's Guide](https://felipefontoura.com/articles/what-is-spec-driven-development) — the complete method, the four pillars, and when to skip it
- [Case study: 13 apps in 70 days, solo, with SDD](https://felipefontoura.com/articles/spec-driven-development-case-study) — the production build this kit came out of
- [How to write a spec an AI can build from](https://felipefontoura.com/articles/how-to-write-a-spec) — the EARS format and copy-paste templates
- [felipefontoura/sdd-book](https://github.com/felipefontoura/sdd-book)

## Acknowledgements

Special thanks to the [Compozy skills](https://github.com/compozy/compozy/tree/main/skills) project. Its skill design demonstrates an excellent level of technical rigor, operational quality, explicit gates, verification discipline, and practical AI workflow structure. This package was inspired by that quality bar and adapts similar principles to a lightweight SDD workflow for Pi.

---

## Why use this

AI can accelerate development, but it can also accelerate ambiguity. This kit enforces a simple discipline:

1. explore before planning;
2. define **WHAT/WHY** before **HOW**;
3. break implementation into verifiable tasks;
4. implement only after human approval;
5. review the delivery against approved artifacts.

The result is less rework, less implicit scope, and more predictable implementation.

---

## How it compares to Spec Kit and Kiro

GitHub Spec Kit and AWS Kiro popularized Spec-Driven Development, and both are excellent. Pi SDD Kit makes a few deliberately different design choices, tuned for a solo-to-small-team operator working across many sessions:

- **Steering as durable project memory.** Global context — product, stack, conventions, principles — lives in `.ai/steering/`, separate from per-feature specs, so the agent reloads the same project memory every session instead of re-deriving it. This fixes "the AI forgets everything between chats" at the project level, not just per feature.
- **`.status` is the only gate.** A one-line `.status` file per feature is the single source of truth for approval. The existence of a `design.md` never counts as approval — only the status token does. That is a harder guarantee than "the file is there, so it must be done."
- **EARS by default.** Functional requirements are written in the Easy Approach to Requirements Syntax, so they are unambiguous enough for an agent to execute without guessing.
- **Clarification and readiness checks are embedded, not extra phases.** Guided decisions (2–4 concrete options plus their impact) live inside the PRD step; the implementation readiness check lives inside TASKS. Fewer commands, same rigor.
- **Handoffs are contracts between stages.** Optional upstream (`strategy-brief.md`) and downstream (`sdd-brief.md`) briefs let SDD plug into a larger multi-package pipeline without bypassing its gates.
- **Lightweight and language-aware.** Plain-markdown skills for small and medium projects — no heavyweight tooling — that write artifacts in your chat language while keeping paths, status values, and IDs canonical in English.

If you want the enterprise-scale, IDE-integrated experience, reach for Spec Kit or Kiro. If you want a transparent, file-based, gate-enforcing workflow you can read and modify, this is that.

---

## Installation

From npm:

```bash
pi install npm:@felipefontoura/pi-sdd-kit
```

Then reload Pi:

```text
/reload
```

---

## Available skills

This package is intended to be used through SDD-prefixed Pi skill commands: `/skill:sdd-*`.

```text
/skill:sdd-init
/skill:sdd-steering
/skill:sdd-idea
/skill:sdd-plan
/skill:sdd-prd
/skill:sdd-spec
/skill:sdd-tasks
/skill:sdd-exec
/skill:sdd-review
/skill:sdd-status
```

### `/skill:sdd-init`

Initializes the project AI/SDD workspace.

Typical structure:

```text
.ai/
  steering/
  sdd/
```

Use this when adopting the workflow in a new or existing project.

---

### `/skill:sdd-steering`

Creates or updates reusable global context in:

```text
.ai/steering/
```

Examples:

```text
.ai/steering/product.md
.ai/steering/tech-stack.md
.ai/steering/conventions.md
.ai/steering/principles.md
.ai/steering/lp.md
```

Use it for product vision, stack, conventions, project principles, UX rules, landing page rules, business domain guidance, or any context reused by multiple skills.

---

### `/skill:sdd-idea`

Explores a raw idea before turning it into a plan or requirements.

Use it when you are still thinking and want cognitive clarity.

Typical output:

```text
.ai/sdd/ideas/001-feature-idea.md
```

---

### `/skill:sdd-plan`

Creates or updates a project/product plan.

Optional for small changes and recommended for medium projects with multiple features, phases, or dependencies.

Typical output:

```text
.ai/sdd/PLAN.md
```

---

### `/skill:sdd-prd`

Creates `requirements.md` for a feature.

Focuses on **WHAT/WHY**:

- users;
- user stories;
- acceptance criteria;
- EARS-style functional requirements;
- non-functional requirements;
- explicit out-of-scope boundaries;
- guided requirement questions and recorded decisions when ambiguity matters.

Typical output:

```text
.ai/sdd/specs/001-feature-name/requirements.md
.ai/sdd/specs/001-feature-name/.status
```

Feature IDs are assigned from the actual directories under `.ai/sdd/specs/` using the next available numeric prefix. `.ai/sdd/INDEX.md` is a dashboard, not the numbering source.

---

### `/skill:sdd-spec`

Creates `design.md` from approved requirements.

Focuses on **HOW**:

- architecture;
- components/modules;
- state/data;
- APIs/integrations;
- security/permissions;
- edge cases;
- technical decisions;
- verification strategy.

Typical output:

```text
.ai/sdd/specs/001-feature-name/design.md
```

---

### `/skill:sdd-tasks`

Creates `tasks.md` from an approved design.

Tasks are small, dependency-aware, verifiable, and traceable to requirements. This step also performs the implementation readiness check, so users do not need a separate analysis command.

Typical output:

```text
.ai/sdd/specs/001-feature-name/tasks.md
.ai/sdd/handoff/sdd-brief.md   # after tasks:approved
```

---

### `/skill:sdd-exec`

Executes an approved task.

The skill should:

- require `tasks:approved`;
- keep scope limited to the selected task;
- follow project conventions;
- run verification;
- update progress only with evidence.

---

### `/skill:sdd-review`

Reviews implementation against:

- `requirements.md`;
- `design.md`;
- `tasks.md`;
- produced code;
- verification evidence.

Typical output:

```text
.ai/sdd/specs/001-feature-name/review.md
.ai/sdd/handoff/sdd-brief.md   # refreshed after review:done
```

---

### `/skill:sdd-status`

Shows a dashboard of the current SDD state.

Use it to see:

- existing ideas;
- current plan;
- specs in draft/approved/implementation/review states;
- blockers;
- the next safe action.

This is a read-only skill.

---

## User-facing templates

This package includes ready-to-copy templates in:

```text
templates/
```

They are based on the SDD flow and include practical structure inspired by PRD, TechSpec, task, review, issue, and ADR workflows.

Available templates:

```text
templates/sdd-index.md
templates/sdd-workflow.md
templates/steering-product.md
templates/steering-tech-stack.md
templates/steering-conventions.md
templates/steering-principles.md
templates/steering-landing-page.md
templates/idea.md
templates/plan.md
templates/requirements.md
templates/design.md
templates/tasks.md
templates/task.md
templates/review.md
templates/handoff.md
templates/issue.md
templates/adr.md
```

Use them as examples, copy them manually, or let the skills fill equivalent artifacts in the user's chat language.

---

## Artifact structure

The package separates reusable AI context from SDD-specific artifacts.

```text
.ai/
  steering/
    product.md
    tech-stack.md
    conventions.md
    principles.md
    lp.md
  strategy/
    handoff/
      strategy-brief.md          # optional upstream input from pi-strategy or another package
  sdd/
    INDEX.md
    WORKFLOW.md
    PLAN.md
    handoff/
      sdd-brief.md               # downstream SDD output contract
    ideas/
      001-feature-idea.md
    specs/
      001-feature-name/
        .status
        requirements.md
        design.md
        tasks.md
        review.md
        decisions.md
```

### `.ai/steering/`

Reusable context for any skill or AI workflow.

Examples:

- product vision;
- personas;
- stack;
- verification commands;
- architecture conventions;
- landing page rules;
- copywriting rules;
- accessibility standards.

### `.ai/sdd/`

Artifacts specific to the Specification-Driven Development workflow.

### Optional upstream handoff

When present, SDD skills may read:

```text
.ai/strategy/handoff/strategy-brief.md
```

This file is optional. It can seed `/skill:sdd-idea`, `/skill:sdd-plan`, or `/skill:sdd-prd`, but it does **not** bypass SDD approval gates.

### SDD handoff output

After approved tasks, and again after completed review, SDD can write or refresh:

```text
.ai/sdd/handoff/sdd-brief.md
```

This is the consolidated output contract for downstream agents/packages. It summarizes source inputs, approved requirements, design decisions, task order, verification plan, review status, blockers, and readiness while preserving links to the original artifacts.

---

## Workflow states

Each feature spec uses a `.status` file with one of these values:

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

Drafts may be saved before approval, but **drafts do not unlock gates**. Skills must validate `.status` before advancing a phase; artifact existence alone never counts as approval.

---

## Human gates

The kit is designed to preserve human decision points.

```text
requirements:draft   → human approval → requirements:approved
design:draft         → human approval → design:approved
tasks:draft          → human approval → tasks:approved
tasks:approved       → implementation allowed
implementation:done  → review
```

Important rules:

- do not implement before `tasks:approved`;
- do not treat drafts as approved artifacts;
- do not silently change requirements or design during implementation;
- do not claim completion without fresh verification evidence.

---

## Traceability

Templates use stable IDs:

```text
US-001   User Story
FR-001   Functional Requirement
NFR-001  Non-Functional Requirement
TD-001   Technical Decision
T1       Task
```

They also include mappings for:

- requirements → design;
- requirements → tasks;
- requirements/tasks → review;
- SDD handoff → requirements, design, tasks, review, and `.status`.

This helps both humans and AI notice uncovered requirements or implementation drift.

---

## Workflow guide

For a copyable user-facing guide to the SDD flow, see:

```text
templates/sdd-workflow.md
```

It documents the simple flow, gates, status rules, feature IDs, steering context, and recommended next actions.

It also makes explicit that clarification and analysis/checklist behavior are embedded in existing phases (`PRD` and `TASKS`) instead of extra public commands.

## Recommended quickstart

### 1. Initialize the project

```text
/skill:sdd-init
```

### 2. Create reusable context

```text
/skill:sdd-steering
```

For example: `product.md`, `tech-stack.md`, `conventions.md`, and optional `principles.md`.

### 3. Explore an idea

```text
/skill:sdd-idea
```

### 4. Plan if needed

```text
/skill:sdd-plan
```

For small features, you can go directly to PRD.

### 5. Create requirements

```text
/skill:sdd-prd
```

### 6. Create technical design

```text
/skill:sdd-spec
```

### 7. Break into tasks

```text
/skill:sdd-tasks
```

### 8. Execute incrementally

```text
/skill:sdd-exec
```

### 9. Review

```text
/skill:sdd-review
```

### 10. Check status anytime

```text
/skill:sdd-status
```

---

## When to use PLAN

Use `/skill:sdd-plan` when there are:

- multiple features;
- delivery phases;
- dependencies between modules;
- different personas;
- unclear MVP boundaries;
- risk of uncontrolled scope growth.

Skip PLAN for:

- small adjustments;
- isolated screens;
- well-bounded changes;
- simple bug fixes.

---

## Example: small flow

```text
/skill:sdd-init
/skill:sdd-prd      → creates requirements.md
/skill:sdd-spec     → creates design.md
/skill:sdd-tasks    → creates tasks.md
/skill:sdd-exec     → implements T1
/skill:sdd-review   → validates delivery
```

## Example: medium flow

```text
/skill:sdd-init
/skill:sdd-steering
/skill:sdd-idea
/skill:sdd-plan
/skill:sdd-prd
/skill:sdd-spec
/skill:sdd-tasks
/skill:sdd-exec
/skill:sdd-status
/skill:sdd-review
```

---

## Philosophy

This kit follows a few principles:

- **The spec is a contract, not decoration.**
- **Code is a consequence of the spec.**
- **Human approval is a gate, not a formality.**
- **Draft does not mean approved.**
- **Tasks must be verifiable.**
- **Review should validate against artifacts, not only opinion.**
- **Global context belongs in `.ai/steering/`, not in every feature.**
- **Handoffs are contracts between workflow stages, not replacements for source artifacts.**

---

## Package development

Validate package contents:

```bash
npm pack --dry-run
```

Package structure:

```text
skills/
  _shared/references/sdd-practical.md
  _shared/references/templates.md
  sdd-init/SKILL.md
  sdd-steering/SKILL.md
  sdd-idea/SKILL.md
  sdd-plan/SKILL.md
  sdd-prd/SKILL.md
  sdd-spec/SKILL.md
  sdd-tasks/SKILL.md
  sdd-exec/SKILL.md
  sdd-review/SKILL.md
  sdd-status/SKILL.md
templates/
  README.md
  requirements.md
  design.md
  tasks.md
  review.md
  handoff.md
  adr.md
  ...
```

---

## License

MIT
