# Stage 9 — Lovable UI Prompts

Write these files only after `01-lovable-design-system-prompt.md` exists.

Create `product-design/NN-slug/02-ui-prompts/`.

- One English file per required screen: `SC-01-<english-slug>.md`.
- The slug matches the English name in section 4.
- Group screens in one file only when they are one tight interaction, such as a page and its only dialog, and say why in the first paragraph. Do not merge unrelated screens.
- Order files by the `F-xx` journeys. Write a repeated screen once.
- A screen marked **محجوبة** gets no invented prompt. Record the `SC-xx` and the blocking `Q-xx` in section 4, ask that question in Arabic, and continue with the other screens.
- Do not call Lovable. Do not say a prompt was executed.
- Do not add `00-coverage-ar.md` or any other extra file.

Read sections 4 through 7 of `00-analysis-ar.md` and the shared-component list in the Design
System prompt. Do not generate code, HTML, or wireframes.

## Each file

The file is English from the first line. It must stand alone. Include only sections that apply
to this screen. Arabic text appears only as interface copy required by the analysis, inside
quotes.

```markdown
# SC-01 — <English screen name>

Build this screen in the existing Lovable project. Follow the established Design System prompt.
Use its shared tokens and components. Do not restyle the project and do not restate that prompt here.

## Purpose

## Actor and permissions

## Workflow

## Layout and hierarchy

## Components

## Information displayed

## Actions

## Forms and fields

## Validation

## States

## Navigation

## Responsive behavior

## Language and direction

## Accessibility

## Business rules on this screen

## Restrictions

## Acceptance criteria
```

Rules for the body:

- Use the same `SC-xx` IDs, actions, permissions, and destinations as the analysis.
- Tell Lovable to follow the Design System, stay consistent with the other screens, keep
  confirmed brand rules, and implement only the actions and states in this prompt.
- Do not paste the Design System prompt into the file.
- Where `Q-xx` remains, say the fact is unresolved and do not invent the business rule.
- If interface language or RTL is not confirmed, say it is not confirmed and do not set a direction.
- Restrictions must forbid features, screens, fields, roles, and status values this screen does
  not list.

## Check before finishing

Compare section 4 with the files. Every non-blocked `SC-xx` has one prompt. No prompt uses an ID
that is absent from the inventory. Navigation matches section 6. Shared component names match
stage 8. No prompt contradicts the Design System or adds a business rule. Every prompt file is
English. If a check fails, fix the file. Tell the user the result in a short Arabic summary.
Do not write that summary into the run folder.
