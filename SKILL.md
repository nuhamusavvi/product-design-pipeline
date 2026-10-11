---
name: product-design-pipeline
description: Turns project requirements, including multiple Plane tasks for one project, into English Lovable prompts and one English backend handoff. Analysis stays in Arabic. Stage 0 consolidates the tasks, stage 8 writes the Design System prompt, stage 9 writes one English UI prompt per screen, and stage 10 writes the backend handoff. Questions to the user are in Arabic. Use when the user asks to analyze requirements, collect Plane tasks, prepare Lovable prompts, or hand a product to a backend developer. Does not generate HTML, wireframes, or a documentation site, and does not claim Plane or Lovable was used unless that access actually succeeded.
metadata:
  domain: workflow
  role: product analyst
  scope: requirements-to-lovable-prompts-and-backend-handoff
  output-format: Arabic analysis, English Design System prompt, English UI prompts, English backend handoff
---

# Product Design Pipeline

Turn project requirements into prompts the user can paste into Lovable, then one English backend
handoff. Lovable builds the interface. This skill does not design the UI, write frontend code, or
operate a Lovable project.

Plane is only a stage 0 source. Read a task only when its text was pasted or a Plane tool in this
session actually returned it. Plane is not assumed to be configured. Do not invent a Plane tool,
retry a connection, or change Plane configuration. Do not call Lovable.

## Copies

- Edit only `D:\Skills\product-design-pipeline`.
- Runtime copy: `C:\Users\Nuha\.cursor\skills\product-design-pipeline`.
- Do not modify `C:\Users\Nuha\.claude\skills\product-design-pipeline`.
- Paths below are relative to the folder that contains this file.

## Language

- Questions, options, and short reasons are clear Arabic. At most four questions in a batch.
- `00-analysis-ar.md` is Arabic.
- `01-lovable-design-system-prompt.md` and every file in `02-ui-prompts/` are English. Arabic
  product labels may appear inside those prompts only as UI copy the analysis requires.
- `03-backend-handoff-en.md` is English. Do not write a second copy in Arabic.

## Outputs

```text
product-design/NN-slug/
  00-analysis-ar.md
  01-lovable-design-system-prompt.md
  02-ui-prompts/SC-01-<slug>.md
  03-backend-handoff-en.md
```

Create a file only when its stage is reached. No PRD, BRD, SRS, data model, API spec, user
stories, test document, wireframe, HTML prototype, gallery, documentation site, or style picker.

## Run setup

1. Next run number: highest `NN-` folder in `./product-design/`, plus one. Missing folder means `01`.
2. Slug: kebab-case English from the product name, or a temporary slug marked **مؤقت**. Do not
   stop to ask for a name.
3. Create `./product-design/NN-slug/` and tell the user the path in one Arabic sentence.
4. Do not write into an older run. A folder with `00-run-log.md` from the old pipeline is not
   resumed.

On `resume`, or when `00-analysis-ar.md` has open stages, continue at the first unfinished stage.
Do not repeat a question the analysis already answers.

## Stages

This table is the only stage order. Load a reference at that stage, not before. Stop after stage 10.

| # | Stage | Output | Reference |
|---|-------|--------|-----------|
| 0 | Requirements Intake | Arabic summary in `00-analysis-ar.md` | `references/intake-questions.md`, `references/analysis-ar.md` |
| 1 | Scope and Functional Requirements | Same file | `references/analysis-ar.md` |
| 2 | Actors and Permissions | Same file | `references/analysis-ar.md` |
| 3 | Business Workflows | Same file | `references/analysis-ar.md` |
| 4 | Screen Inventory | Same file. IDs are `SC-xx` | `references/analysis-ar.md` |
| 5 | UI States and Validation Behavior | Same file | `references/analysis-ar.md` |
| 6 | User Flows and Navigation | Same file. Fix inventory gaps before leaving | `references/analysis-ar.md` |
| 7 | UI Specification and Prompt Preparation | Same file | `references/analysis-ar.md` |
| 8 | Lovable Design System Prompt | `01-lovable-design-system-prompt.md` in English | `references/lovable-design-system.md` |
| 9 | Lovable UI Prompts | One English file per required screen | `references/lovable-ui-prompts.md` |
| 10 | Consolidated Backend Handoff | `03-backend-handoff-en.md` | `references/backend-handoff.md` |

Stage 8 is finished before stage 9. Stage 10 is last. Stages 1–7 add sections to the analysis.
They do not reread Plane and they do not restate section 0.

Continue while the information is enough. Ask in Arabic only when an answer would otherwise be
invented and would change the screens, the prompts, or the handoff. Do not ask for approval
after each stage. Non-blocking gaps stay as `Q-xx`. Scope defaults to MVP and does not delete a
requirement the source stated.

## IDs

Permanent once written. Never renumber them.

| Prefix | Meaning | Assigned |
|--------|---------|----------|
| `Q-xx` | Open question | Any stage |
| `A-xx` | Assumption, not confirmed | Any stage |
| `P-xx` | Actor | Stage 2 |
| `FR-xx` | Functional requirement | Stage 1 |
| `BR-xx` | Stated business rule | Stage 1 or 3 |
| `W-xx` | Business workflow | Stage 3 |
| `SC-xx` | Screen | Stage 4 |
| `F-xx` | User journey | Stage 6 |

Plane task identifiers stay as given. Traceability is `task id → FR-xx → SC-xx`, and
`W-xx → F-xx → SC-xx`.

## Plane

Several task IDs, links, or pasted tasks are one project unless the user separates them. Merge
duplicates, keep details, and record conflicts. Do not make one screen or one pipeline run per
task. A task that is a bug, a question, or unrelated stays in the source table and is not turned
into a requirement.

If a named task has no text and no Plane tool returned it, list it as unread, say so in Arabic,
and do not describe it. Consolidate what was actually read before stage 1. Details are in
`references/intake-questions.md`.

## Do not

- Generate the excluded deliverables listed under Outputs.
- Call Lovable or say a prompt was executed.
- Claim a Plane task was read when it was not.
- Invent requirements, roles, permissions, statuses, screens, brand colors, fonts, schemas,
  endpoints, or authentication.
- Use a style library or a style picker.
- Assume right-to-left layout unless the requirements support it.
- Repeat an answered question, or ask more than four at once.
