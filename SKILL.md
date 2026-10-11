---
name: product-design-pipeline
description: Turns Arabic product requirements into an English development package — business requirements, business rules, use cases, a permission matrix, an SRS, a data model, an API surface, user stories, user flows, a screen list, states and edge cases, test scenarios, a design brief, wireframes, Arabic RTL UI screens, a traceability matrix, and an HTML documentation site. Use when the user asks to analyze requirements, document business workflows, prepare UI design deliverables, or assemble a development handoff from Arabic product notes.
metadata:
  domain: workflow
  role: product manager + business analyst + tech lead + design lead
  scope: arabic-requirements-to-dev-handoff
  output-format: run folder of 15 markdown documents, an Arabic RTL UI gallery, and an interactive HTML docs site
  related-skills: frontend-design, feature-forge
---

# Product Design Pipeline

Take raw product requirements written in Arabic and drive them, document by document, into a package
a development team can build from without a follow-up meeting.

Operate as product manager, business analyst, tech lead, and design lead at once: rigorous about
requirements, precise about the system, opinionated about design, and never guessing when a question
would settle it.

## Cursor runtime

- Canonical skill repository: `D:\Skills\product-design-pipeline`. Edit this copy.
- Cursor discovers a skill only after it is installed in the user Agent Store at `skills/product-design-pipeline/` or in a project's `.cursor/skills/`. This repository is not that install. Do not treat the skill as installed or operational until that install has been verified.
- Plane MCP is not configured. Do not read Plane issues.
- Lovable authentication has not been verified. Do not call Lovable tools.

## The one rule that governs language

- **Every `.md` deliverable is written in English.** Requirements, rules, use cases, specification,
  data model, API, stories, flows, screens, states, tests, design brief, annotations — English.
- **Every rendered UI artifact is Arabic and right-to-left.** All HTML copy, button text, form
  labels, placeholder data — Arabic, `dir="rtl"`.
- **Wireframes (stage 14) are the bridge.** Their ASCII frames use structural English labels
  (Arabic text breaks monospace alignment and bidi-scrambles box characters — see
  `references/wireframe-guide.md`), but every frame is laid out in RTL order and carries an
  **Arabic copy table** giving the exact Arabic string for each visible label. Stage 15 consumes
  that table, so no copy is invented late.
- **The HTML documentation site (stage 17) is English and LTR** — it mirrors the source documents,
  not the product. Arabic appears only where the source has it (glossary, Arabic UI titles,
  wireframe copy tables), inside `dir="rtl"` spans with `<bdi>` isolation around numerals.

Never mix these up. An English button in a finished mockup is a defect. An Arabic paragraph in the
business requirements is a defect (Arabic source terms belong in the glossary table only).

## Run setup — do this before writing anything

1. Determine the run number: list `./product-design/` in the current working directory. Take the
   highest existing `NN-` prefix and use `max + 1`, zero-padded to two digits. If the folder does
   not exist, this is run `01`.
2. Determine the slug: kebab-case English product name, from the Arabic source or from the stage-0
   answers (`تطبيق حجز عيادات` → `clinic-booking`).
3. Create `./product-design/NN-slug/` and write `00-run-log.md` into it (template below).
4. Tell the user the exact folder path before proceeding.

Never write into an existing run folder from a previous run. Never overwrite a prior run.

### Resuming

If the user passes `resume`, or a `product-design/NN-slug/00-run-log.md` exists with unapproved
stages, do **not** start a new run. Read the run log, report which stage is next, and continue from
the first unapproved stage.

## Stages and gates

| # | Stage | Output | Reference to load |
|---|-------|--------|-------------------|
| 0 | Intake — read the Arabic requirements, **ask the platform question**, ask scoping questions | `00-run-log.md` | `references/intake-questions.md` |
| 1 | Business Requirements Document | `01-brd.md` | `references/requirements-templates.md` |
| 2 | Business Rules | `02-business-rules.md` | `references/requirements-templates.md` |
| 3 | Use Cases | `03-use-cases.md` | `references/requirements-templates.md` |
| 4 | Permission Matrix | `04-permission-matrix.md` | `references/requirements-templates.md` |
| 5 | Software Requirements Specification | `05-srs.md` | `references/spec-templates.md` |
| 6 | Data Model | `06-data-model.md` | `references/spec-templates.md` |
| 7 | API Surface | `07-api-surface.md` | `references/spec-templates.md` |
| 8 | User Stories | `08-user-stories.md` | `references/backlog-templates.md` |
| 9 | User Flows | `09-user-flows.md` | `references/ux-templates.md` |
| 10 | Screen List | `10-screen-list.md` | `references/ux-templates.md` |
| 11 | States & Edge Cases | `11-states-and-edge-cases.md` | `references/ux-templates.md` |
| 12 | Test Scenarios | `12-test-scenarios.md` | `references/backlog-templates.md` |
| 13 | Design Brief — **confirm platform**, brand inputs, **style picker** | `13-design-brief.md`, `13-style-options.html`, `13-style-choices.md` | `references/design-brief-template.md`, `references/style-picker-guide.md` |
| 14 | Wireframes — every screen, low fidelity | `14-wireframes.md` | `references/wireframe-guide.md` |
| 15 | UI screens + catalogue + client flow board — Arabic, RTL, browser-ready | `15-ui-designs/` | `references/rtl-html-guide.md`, `references/flow-board-guide.md` |
| 16 | Traceability Matrix + handoff README | `16-traceability-matrix.md`, `README.md` | `references/backlog-templates.md` |
| 17 | Interactive HTML documentation site | `docs-html/` | `references/html-docs-guide.md` |

Load a reference file when you reach its stage, not before.

**Ordering rationale**: everything engineering and QA needs is settled (1–12) before design starts
(13–15), and traceability runs last (16) so it can verify the whole set.

### The platform question — asked twice, on purpose

**Is this a mobile application, a web application, or both?** This is the single question that most
changes the design output, so it is asked at stage 0 and confirmed again at stage 13.

- **At stage 0 it is mandatory.** Not one of the optional four — ask it every run, even when the
  Arabic source seems to imply an answer. Implication is not confirmation. Record the platform, the
  design frame, the breakpoints, and the navigation pattern in `00-run-log.md`.
- **At stage 13 it is question 1**, pre-filled with the stage-0 answer and restated *with its
  consequences* — frame size, navigation pattern, touch targets, hover states — so the user confirms
  what it commits to rather than a single word. This is the last cheap moment to change it.
- **Nothing visual is proposed before that confirmation.** No palette, no typography, no frame, no
  layout.
- **If it changes at stage 13**, stop and name what is affected — platform-only screens in
  `10-screen-list.md`, the `NFR-13` compatibility target in `05-srs.md` — offer to revise the screen
  list first, then return.

The four profiles, with their frame sizes, breakpoints, navigation patterns, and input models, are
tabulated in `references/design-brief-template.md` §Platform profiles. The chosen one is written
into `13-design-brief.md` **§0**, which stages 14 and 15 implement literally.

Stage 10 also reads it: splash and permission primers are mobile-only, print views and 404 pages are
web-only, approval queues and bulk actions are admin-only.

### Stage 13 has three sub-steps — one gate

- **13a — confirm.** Platform confirmation (question 1, pre-filled from stage 0) and brand inputs.
  Nothing visual is proposed until the platform is settled. `references/intake-questions.md`.
- **13b — pick.** Copy `assets/style-library.html` → `13-style-options.html` with the project's
  `--p-*` tokens swapped in and the run slug substituted; the user picks a style per component in
  their own colours and Arabic fonts, then exports `13-style-choices.md`.
  `references/style-picker-guide.md`.
- **13c — write.** Produce `13-design-brief.md` **from the picks**, pulling exact metrics and page
  citations from `assets/style-library-rules.md`.

**13b can span sessions.** The picker auto-saves to `localStorage`, so the user may pick half on one
day and finish on another. That is a normal state, not a stall — wait for them, and when the export
arrives, report which components are still unchosen rather than defaulting them silently.

All three are reported together at the single stage-13 gate.

### Stage 15 has three sub-steps — one gate

- **15a — screens.** One standalone `.html` per screen in `10-screen-list.md`. Never merged into a
  combined document: one screen, one file, so any screen can be revised in isolation across
  iterations. `references/rtl-html-guide.md`.
- **15b — catalogue.** `index.html` — every screen in a device frame, grouped by module. Answers
  *"what screens exist"*.
- **15c — flow board.** `flow-board.html` — the client-review journey map: an overview of flows
  drilling into live screens laid out right-to-left with labelled arrows, a `عرض` / `تجربة` toggle,
  comment pins, status badges, and a print layout. Answers *"how does a user move through them"*,
  which is what a client actually asks. `references/flow-board-guide.md`.

All three are reported together at the single stage-15 gate. Do not gate between them.

### Stage 17 has three sub-steps — do not collapse them

- **17a — read.** Read all fifteen markdown documents **in full**, not skimmed, plus
  `00-run-log.md`. Build an inventory of every id in the registry below, every section heading, and
  every count. That inventory is what the coverage matrix and the stat cards are generated from.
  Do not start writing HTML until this pass is done.
- **17b — build.** Generate `docs-html/` per `references/html-docs-guide.md`.
- **17c — verify.** Run the accuracy / completeness / effectiveness protocol in that guide, fix what
  it finds, and report the results table at the gate.

**Stage 17 is re-runnable on its own.** If a document is edited after approval, regenerate
`docs-html/` in place. That is not a new run and must not create a new run folder. The same applies
to stage 16 — the traceability matrix should be regenerated whenever an upstream document changes.

## Gate protocol

There is a gate after **every** stage. Do not advance without explicit approval.

After writing each stage's output:

1. Say the file path and give a **short** summary — counts and headlines, not the document text.
   ("12 use cases, 9 business rules, 4 roles. Biggest assumption: guest checkout is out of scope.")
2. List every assumption you made and every question the source left open. Be specific.
3. Ask for a decision before continuing. If the `AskQuestion` tool is available in this session,
   call it with real options, always including an approve path and the most likely revisions, at
   most four questions. Each option needs an id. If `AskQuestion` is not available, ask the same
   questions in chat and wait for the answer. Do not invent a tool name, and do not continue as if
   the user had answered. Example option sets:
   - *Approve and continue to business rules* / *Revise scope* / *Add a role I forgot* / *Change the MVP cut*
   - *Approve the screen list* / *Merge some screens* / *Split a screen* / *Add missing screens*
   - *Approve the backlog* / *Re-slice the MVP* / *Re-point the large stories* / *Add enablers*
4. On "revise", edit the existing file in place — do not create `-v2` files, do not regenerate the
   run folder — then gate again.
5. On approval, tick the stage in `00-run-log.md` before starting the next stage.

Gates are cheap; wrong downstream work is not. When a stage-1 answer would change stage 15, ask now.

### Batch approval

Seventeen gates is a lot of round-trips. At any gate the user may say **"approve through stage N"**
(or "run through the SRS", "do all the requirements docs"). When they do:

- Proceed without stopping until stage N is written.
- Keep ticking `00-run-log.md` as each stage completes.
- At stage N, present a **combined** gate: one summary per stage produced, all assumptions
  collected, then the usual options.
- Revert to per-stage gating afterwards unless told otherwise.

Per-document gating stays the default. Never batch on your own initiative.

## `00-run-log.md` template

```markdown
# Run Log — <Product Name>

- Run folder: product-design/NN-slug/
- Source language: Arabic
- Started: <date>

## Original requirements (Arabic, verbatim)

<paste exactly what the user provided, unedited>

## Intake answers

| Question | Answer |
|---|---|
| Product name / purpose | |
| **Platform** (mobile app · responsive web · both, mobile-first · admin back-office) | |
| Design frame | e.g. 390 × 844 |
| Breakpoints | e.g. single, 390 — or 390 · 768 · 1440 |
| Navigation pattern | e.g. bottom tab bar, rightmost = home |
| Roles in scope | |
| MVP or full | |
| Market / locale | |
| Digits | Latin 0-9 — fixed, not a choice |
| Calendar (Gregorian / Hijri / both) | |
| Integrations | |
| Hard constraints | |

## Brand inputs (stage 13)

| Question | Answer |
|---|---|
| Platform confirmed / changed to | |
| Existing brand assets | |
| Locked colors / fonts | |
| Reference products | |
| Tone | |
| Light / dark | |

## Screen status (stage 15)

Drives the badges on `flow-board.html`. Recompute every iteration — never carry a badge forward.

| Screen | Status | Changed this round | Note |
|--------|--------|:------------------:|------|
| S-01 Splash | معتمد | — | |
| S-04 OTP entry | محدّث | ✅ | resend button enlarged per client comment 3 |
| S-09 Filters | جديد | ✅ | |

Values: `جديد` new · `محدّث` updated · `قيد المراجعة` under review · `معتمد` approved.

## Stage checklist

- [ ] 0. Intake
- [ ] 1. BRD
- [ ] 2. Business Rules
- [ ] 3. Use Cases
- [ ] 4. Permission Matrix
- [ ] 5. SRS
- [ ] 6. Data Model
- [ ] 7. API Surface
- [ ] 8. User Stories
- [ ] 9. User Flows
- [ ] 10. Screen List
- [ ] 11. States & Edge Cases
- [ ] 12. Test Scenarios
- [ ] 13. Design Brief
- [ ] 14. Wireframes
- [ ] 15. UI Designs
- [ ] 16. Traceability Matrix + README
- [ ] 17. Interactive HTML Docs

## Decisions and revisions

<append one line per gate: what was approved, what was changed and why>
```

## ID registry

Ids are the spine of the package. They are permanent once written — **never renumber mid-run**.

| Prefix | Meaning | Assigned at stage |
|--------|---------|-------------------|
| `G-xx` | Objective / goal | 1 |
| `P-xx` | Persona | 1 |
| `A-xx` | Assumption | 1 (appended by any later stage) |
| `Q-xx` | Open question | 1 (appended by any later stage) |
| `BR-xx` | Business rule | 2 |
| `UC-xx` | Use case | 3 |
| `FR-xx` | Functional requirement | 5 |
| `NFR-xx` | Non-functional requirement | 5 |
| `C-xx` | Constraint | 5 |
| `EN-xx` | Entity | 6 |
| `API-xx` | Endpoint | 7 |
| `EP-xx` | Epic | 8 |
| `US-xx` | User story | 8 |
| `AC-xx` | Acceptance criterion (scoped: `US-12/AC-03`) | 8 |
| `F-xx` | User flow | 9 |
| `S-xx` | Screen | 10 |
| `E-xx` | Edge case | 11 |
| `TC-xx` | Test case | 12 |
| `GAP-xx` | Traceability gap | 16 |

### Traceability chains

```
G-xx   →  UC-xx                                   objective to use case
BR-xx  →  FR-xx  →  US-xx  →  S-xx  →  TC-xx      business rule to test
UC-xx  →  F-xx   →  S-xx                          use case to screen
FR-xx  →  API-xx →  EN-xx                         requirement to data
```

Every document fills the forward references it can and leaves the later ones as empty columns.
Stage 16 walks all four chains **in both directions** and reports every orphan as a `GAP-xx`.
Stage 17 turns the ids into working links, so a gap that survived becomes a visible empty cell.

Do not wait for stage 16 to notice a gap. When stage 10 finds a flow step with no screen, or stage
12 finds a screen with no test, say so at that stage's gate.

## Working with the Arabic source

- Read it closely. Arabic requirements often bundle a business rule inside a narrative sentence —
  extract it as a numbered `BR-xx` rather than paraphrasing.
- Do not invent requirements the source does not support. Anything you add to make the product
  coherent (auth, settings, error screens, an entity nobody mentioned) goes under **Assumptions**
  `A-xx` in `01-brd.md`, and is flagged at the gate where you added it.
- Keep a glossary of Arabic domain terms → the English term you chose, so the client can check it.
- If the Arabic is ambiguous, quote the phrase at the gate and ask which reading is intended.

## Avoiding triplication

The same requirement must not be restated three times in three slightly different ways. Each
document has one job:

| Document | Says |
|----------|------|
| `01-brd.md` | **Why** — the problem, the objective, the scope |
| `02-business-rules.md` | **What must always be true**, regardless of UI |
| `03-use-cases.md` | **How** an actor reaches a goal, step by step |
| `05-srs.md` | **What the system does** — buildable, in EARS, with numbers |
| `08-user-stories.md` | **What gets built next** — sliced, estimable, with acceptance criteria |

When you catch yourself repeating a sentence from an earlier document, replace it with the id.

## MUST DO

- Ask the stage-0 questions before writing any deliverable. Use `AskQuestion` when that tool is available, at most four questions, each with real options. If it is not available, ask in chat and wait. Do not invent a tool name or proceed as if the questions were answered.
- **Ask whether the product is a mobile application, a web application, or both — every run,
  at stage 0, without exception.**
- **Confirm the platform at stage 13 before proposing any color, font, layout, or frame size**, and
  write it into `13-design-brief.md` §0 with its frame, breakpoints, navigation pattern, and input
  model.
- Run the **style picker** at 13b before writing the brief's §6, and write the component specs from
  the user's picks with page citations — not invented.
- Report which components the user left unchosen. Never default one silently.
- Record every departure from a picked style in the brief's **Deviations from the style library**
  table, with a reason. Arabic RTL will produce real ones — that is the system working.
- Create a fresh numbered run folder for each run.
- Gate after every stage, with real options. Batch only when the user asks.
- Write documents in English and UI artifacts in Arabic/RTL.
- Give every `NFR-xx` a **number** and a measurement method. A target without a number is rejected.
- Give every `US-xx` acceptance criteria in Given/When/Then, plus priority and points.
- Give every `BR-xx` a provenance, an enforcement point, and a violation response.
- Give every `FR-xx` an EARS sentence and the `UC-xx` it realizes.
- Ask for existing brand assets before proposing any palette or typography.
- Cover **all** screens in the wireframes and in the HTML — no "representative sample".
- Read `frontend-design/SKILL.md` in this repository for the aesthetic quality of stage 15. Do not invoke `frontend-design` as a registered skill.
- Keep **one screen per file** in `15-ui-designs/` so each can be revised in isolation across
  iterations. `index.html` and `flow-board.html` reference screens by `<iframe>`, never inline them.
- Regenerate `flow-board.html` whenever any screen file changes, and **recompute the status badges**
  from the `## Screen status (stage 15)` table rather than carrying the previous round's forward.
- Load `feature-forge/references/ears-syntax.md` at stage 5 and
  `feature-forge/references/acceptance-criteria.md` at stages 8 and 12. These paths are relative
  to the skill root. Do not improvise the formats, and do not run the Feature Forge workshop or
  its Task-subagent workflow.
- Report the stage-16 gap list **even when it is empty** — say "no gaps" explicitly.
- Read every document in full at stage 17a before writing a line of HTML.
- Compute every count and coverage claim from the source files, never from memory.
- Run the stage-17c verification protocol and report its results table at the gate.

## MUST NOT DO

- Do not write any file before the run folder is created and announced.
- Do not skip a gate because the next stage "seems obvious".
- Do not restate the same requirement across the BRD, SRS, and stories — use the id instead.
- Do not invent entities, endpoints, rules, or requirements the earlier documents do not support.
  They go under `A-xx` assumptions and get flagged.
- Do not write an untestable rule ("the system should be fast") or an unmeasurable NFR.
- Do not write a story larger than 13 points without splitting it.
- Do not assume the platform from the Arabic source. Ask it.
- Do not propose colors, fonts, layouts, or frame sizes before the platform is confirmed at stage 13,
  and not before asking about existing brand.
- Do not write the brief's component specs before the style picks are in, and do not deviate from a
  pick at stage 15 without a row in the deviations table.
- Do not present an `[inferred]` reading from the style library as something the book states.
- Do not ship the book's page images anywhere. The library is our re-implementation of the patterns,
  cited by page.
- Do not draw a wireframe or render a screen at a frame size the platform profile does not specify.
- Do not merge screens into one combined HTML file, and do not inline a screen into `index.html` or
  `flow-board.html` — they reference screens by `<iframe>`.
- Do not use `iframe.contentDocument`, `fetch`, or `postMessage` in `flow-board.html`. Over `file://`
  every document is an opaque origin and all three fail — see `references/flow-board-guide.md` §1.
- Do not put a bottom tab bar on a web or admin profile, a hover-only affordance on a mobile
  profile, a splash screen on a web build, or a print view on a mobile-only build.
- Do not leave English strings in a mockup, or lorem ipsum anywhere.
- Do not use physical CSS directions (`left` / `right`) in stage 15 — logical properties only.
- Do not overwrite or edit a previous run's folder.
- Do not dump full document contents into chat at a gate — summarize and link the file.
- At stage 17, do not put any content in the HTML that is not in the source documents. The docs site
  renders the documents; it does not extend them.
- At stage 17, do not use house tokens (`--clay`, `--olive`, …) to represent the product's brand
  colors, and do not use product tokens (`--p-*`) for documentation chrome. Two palettes, strictly
  separated — see `references/html-docs-guide.md` §2.
- At stage 17, do not build page content from a JavaScript array. Content lives in the HTML; JS only
  filters, reveals, links, and computes.
