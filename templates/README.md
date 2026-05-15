# Pi SDD Kit Templates

These are user-facing templates for projects using Pi SDD Kit.

## Language policy

The templates are written in EN-US as package source. When used by a skill, generated artifacts should be written in the user's initial chat language while preserving canonical identifiers, file names, commands, status values, and IDs.

## Recommended artifacts

```text
.ai/
  steering/
    product.md          <- templates/steering-product.md
    tech-stack.md       <- templates/steering-tech-stack.md
    conventions.md      <- templates/steering-conventions.md
    lp.md               <- templates/steering-landing-page.md
  sdd/
    INDEX.md            <- templates/sdd-index.md
    PLAN.md             <- templates/plan.md
    ideas/
      001-name.md       <- templates/idea.md
    specs/
      001-feature/
        .status
        requirements.md <- templates/requirements.md
        design.md       <- templates/design.md
        tasks.md        <- templates/tasks.md
        review.md       <- templates/review.md
        decisions.md    <- templates/adr.md
```

## Template set

- `sdd-index.md` — dashboard for SDD artifacts.
- `steering-product.md` — reusable product context.
- `steering-tech-stack.md` — reusable technical context.
- `steering-conventions.md` — reusable project conventions.
- `steering-landing-page.md` — optional landing page guidance.
- `idea.md` — divergent idea exploration artifact.
- `plan.md` — project/product plan.
- `requirements.md` — PRD / requirements artifact.
- `design.md` — technical design / spec artifact.
- `tasks.md` — master task plan.
- `task.md` — optional individual task format.
- `review.md` — implementation review artifact.
- `issue.md` — optional review issue format.
- `adr.md` — architecture decision record.
