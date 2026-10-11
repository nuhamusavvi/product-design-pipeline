---
name: product-design-pipeline
description: Turns Arabic product requirements into an English development package. The PRD is the primary product-requirements document; a separate BRD is written only when a business or contractual need exists. The package also includes business rules, use cases, a permission matrix, an SRS, a data model, an API surface, user stories, user flows, a screen list, states and edge cases, test scenarios, a design brief, wireframes, Arabic RTL UI screens, a traceability matrix, and an HTML documentation site. Clarification questions to the user are in Arabic. Use when the user asks to analyze requirements, document business workflows, prepare UI design deliverables, or assemble a development handoff from Arabic product notes.
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
requirements, precise about the system, and opinionated about design. Ask only when the next
decision is blocked. Do not invent a requirement to keep moving, and do not present an assumption
as a confirmed fact.

## Cursor runtime

- Canonical skill repository: `D:\Skills\product-design-pipeline`. Edit this copy.
- Cursor discovers a skill only after it is installed in the user Agent Store at `skills/product-design-pipeline/` or in a project's `.cursor/skills/`. This repository is not that install. Do not treat the skill as installed or operational until that install has been verified.
- Plane MCP is not configured. Do not read Plane issues.
- Lovable authentication has not been verified. Do not call Lovable tools.

## Language

Two languages, used for different jobs. Do not mix them up.

**Talking to the user is Arabic.** Every clarification question, option label, recommendation, and
short note about why a question matters is written in clear, simple Arabic. Avoid formal wording
and complicated technical phrasing. Terms such as API, PRD, Workflow, and UI may stay in English
when that makes the question clearer. Product names, technical identifiers, API names, code
identifiers, and permanent IDs keep their original spelling. Do not ask the user in English by
default. Internal skill instructions and reference files stay in English; that does not apply to
text the user reads.

**Project deliverables are English.**

- **Every `.md` deliverable is written in English.** The PRD, rules, use cases, specification,
  data model, API, stories, flows, screens, states, tests, design brief, annotations, and any
  technical handoff — English.
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

An English button in a finished mockup is a defect. An Arabic paragraph in a project document is a
defect (Arabic source terms belong in the glossary table only). An English clarification question
to the user is a defect.

## Run setup — do this before writing anything

1. Determine the run number: list `./product-design/` in the current working directory. Take the
   highest existing `NN-` prefix and use `max + 1`, zero-padded to two digits. If the folder does
   not exist, this is run `01`.
2. Determine the slug: kebab-case English product name. If the source names the product, use that.
   If it does not, use a temporary descriptive English name and mark it **Provisional** in the run
   log. Do not stop requirements analysis to ask for a name (`نظام صيانة أجهزة` →
   `device-maintenance`).
3. Create `./product-design/NN-slug/` and write `00-run-log.md` into it (template below).
4. Tell the user the exact folder path before proceeding.

Never write into an existing run folder from a previous run. Never overwrite a prior run.

### Resuming

If the user passes `resume`, or a `product-design/NN-slug/00-run-log.md` exists with unapproved
stages, do **not** start a new run. Read the run log, report which stage is next, and continue from
the first unapproved stage. After the user answers a question, fold the answer into the run log and
continue from the stage that was waiting. Do not restart intake, and do not ask a question the run
log already answers.

## Stages and gates

| # | Stage | Output | Reference to load |
|---|-------|--------|-------------------|
| 0 | Intake — read the Arabic requirements, ask only blocking questions | `00-run-log.md` | `references/intake-questions.md` |
| 1 | Product Requirements Document | `01-prd.md` | `references/requirements-templates.md` |
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
| 13 | Design Brief — settle platform if still open, brand inputs, **style picker** | `13-design-brief.md`, `13-style-options.html`, `13-style-choices.md` | `references/design-brief-template.md`, `references/style-picker-guide.md` |
| 14 | Wireframes — every screen, low fidelity | `14-wireframes.md` | `references/wireframe-guide.md` |
| 15 | UI screens + catalogue + client flow board — Arabic, RTL, browser-ready | `15-ui-designs/` | `references/rtl-html-guide.md`, `references/flow-board-guide.md` |
| 16 | Traceability Matrix + handoff README | `16-traceability-matrix.md`, `README.md` | `references/backlog-templates.md` |
| 17 | Interactive HTML documentation site | `docs-html/` | `references/html-docs-guide.md` |

Load a reference file when you reach its stage, not before.

**Ordering rationale**: everything engineering and QA needs is settled (1–12) before design starts
(13–15), and traceability runs last (16) so it can verify the whole set.

### Platform

The platform changes screens, navigation, and the design frame. Do not silently assume one when
that choice would change the design. Do not ask it on every run, and do not ask it twice.

- If the source already states the platform, record it as **Confirmed** and do not ask.
- If it is unspecified and the current stage does not depend on it, record an open question in
  `01-prd.md` §8 and continue. Do not block the PRD on it.
- Ask, in Arabic, when the next design decision needs it — usually the screen list (stage 10) or
  the design brief (stage 13) — and only if it is still unanswered. Explain briefly why it matters.
  Options, in this order:
  - تطبيق موبايل
  - تطبيق ويب
  - الاثنين معاً
  - غير محسوم حالياً
- **غير محسوم حالياً** keeps the question open. Do not invent a platform. Stop before wireframes or
  UI screens until one is chosen, because those artifacts need a frame.
- After the user answers, record the platform, the design frame, the breakpoints, and the
  navigation pattern in `00-run-log.md`. Do not ask again.
- Map a confirmed choice onto one row in `references/design-brief-template.md` §Platform profiles
  and write that profile into `13-design-brief.md` **§0**. A web product that is clearly an internal
  admin tool uses the admin profile; say so in the run log. Do not add a fifth user-facing option
  unless that split is itself a blocking decision.
- **Nothing visual is proposed until the platform is settled.** No palette, no typography, no
  frame, no layout.
- **If a confirmed platform later changes**, stop and name what is affected — platform-only screens
  in `10-screen-list.md`, the `NFR-13` compatibility target in `05-srs.md` — offer to revise the
  screen list first, then return.

Stage 10 reads the recorded platform: splash and permission primers are mobile-only, print views
and 404 pages are web-only, approval queues and bulk actions are admin-only. If the platform is
still open at stage 10, ask before adding any platform-only screen.

### Stage 13 has three sub-steps — one gate

- **13a — settle.** If the platform is already confirmed, write it into the brief and do not ask
  again. If it is still open, ask the Arabic platform question and wait. Then ask only the brand
  questions that are still unanswered and that visual design needs. Nothing visual is proposed
  until the platform is settled. `references/intake-questions.md`.
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
2. List every assumption you made and every question the source left open. Be specific. Say which
   items are defaults, which are assumptions, and which are confirmed. Non-blocking open questions
   are reported here; they are not turned into extra questions.
3. Ask for a decision before continuing. The question and every option the user sees are in Arabic.
   If the `AskQuestion` tool is available in this session, call it with real options, always
   including an approve path and the most likely revisions, at most four questions. Each option
   needs an id; labels are Arabic. If `AskQuestion` is not available, ask the same questions in
   Arabic chat and wait for the answer. Do not invent a tool name, and do not continue as if the
   user had answered. Example option labels:
   - موافق، كمّل على قواعد العمل / عدّل النطاق / أضف دور / غيّر حدود النسخة الأولى
   - موافق على قائمة الشاشات / ادمج بعض الشاشات / اقسم شاشة / أضف شاشات ناقصة
   - موافق على قائمة العمل / أعد ترتيب النسخة الأولى / قسّم القصص الكبيرة / أضف شغلاً ناقصاً
4. On "revise", edit the existing file in place — do not create `-v2` files, do not regenerate the
   run folder — then gate again.
5. On approval, tick the stage in `00-run-log.md` before starting the next stage. Fold any answers
   into the documents and continue. Do not restart intake.

Ask a clarification question only when the next stage would otherwise have to invent the answer.
If later work can proceed with the item recorded under Open Questions, do not interrupt.

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
- Document language: English
- User-facing questions: Arabic
- Product name status: Confirmed | Provisional
- Started: <date>

## Original requirements (Arabic, verbatim)

<paste exactly what the user provided, unedited>

## Intake answers

Status is **Confirmed**, **Default**, **Assumption**, or **Open**. A default or an assumption is
not a confirmed requirement. Do not leave a row blank when a documented default applies; write the
default and mark it Default.

| Question | Answer | Status |
|---|---|---|
| Product name / purpose | | |
| Platform (تطبيق موبايل · تطبيق ويب · الاثنين معاً · غير محسوم حالياً) | | |
| Design frame | e.g. 390 × 844 | |
| Breakpoints | e.g. single, 390 — or 390 · 768 · 1440 | |
| Navigation pattern | e.g. bottom tab bar, rightmost = home | |
| Roles in scope | | |
| MVP or full | MVP, unless the user specified otherwise | Default |
| Market / locale | | |
| Digits | Latin 0-9 — fixed, not a choice | Default |
| Calendar (Gregorian / Hijri / both) | | |
| Integrations | | |
| Hard constraints | | |

## Brand inputs (stage 13)

| Question | Answer |
|---|---|
| Platform (use the recorded answer; ask only if still Open) | |
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
- [ ] 1. PRD
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

## Clarification questions

Full worked rules and the device-maintenance example are in `references/intake-questions.md`.
These rules govern every stage:

1. Ask only what the next meaningful decision needs.
2. Before asking, check the supplied requirements and the run log. If the answer is already there,
   use it.
3. If the gap does not block the current stage, record it as `Q-xx` under **Open Questions** in
   `01-prd.md` §8 and continue.
4. Do not ask the user to confirm a reasonable, low-risk default. Scope defaults to **MVP** unless
   the user specified otherwise. When the source is already a small initial scope, do not ask them
   to confirm that default.
5. Use a documented default where one exists. In the run log and in the PRD, mark each item
   **Confirmed**, **Default**, **Assumption**, or **Open**. A default or an assumption is not a
   confirmed requirement.
6. Never invent a business rule, status name, or transition, and never present an assumption as a
   confirmed fact.
7. Group the questions that are genuinely necessary into one batch of at most four.
8. Do not repeat a question the current project already answered.
9. Do not ask the whole pool at the start. Ask when the current stage needs the answer.
10. After the user answers, incorporate the answers and continue from the stage that was waiting.
    Do not restart intake.
11. When a question is necessary, add a short Arabic line on why the answer matters if that is not
    obvious.
12. A non-blocking question does not interrupt the workflow.

When `AskQuestion` is available, use it for those structured questions. The prompt and every
user-facing option are Arabic. Option labels are short. Add **غير ذلك** when the list may not
cover the answer. Mark a justified suggestion with **(مقترح)** and record it as a suggestion, not
as a confirmed requirement, until the user chooses it. Add a defer option when the decision can
stay open. If `AskQuestion` is not available, ask the same questions in Arabic chat and wait. Do
not invent a tool name, and do not continue as if the user had answered.

## Working with the Arabic source

- Read it closely. Arabic requirements often bundle a business rule inside a narrative sentence —
  extract it as a numbered `BR-xx` rather than paraphrasing. If the sentence does not actually
  state the rule, do not write one. Record `Q-xx` instead.
- Do not invent requirements the source does not support. Anything you add to make the product
  coherent (auth, settings, error screens, an entity nobody mentioned) goes under **Assumptions**
  `A-xx` in `01-prd.md`, and is flagged at the gate where you added it.
- Missing statuses, transitions, and other unnamed business rules stay under **Open Questions**.
  Document the behavior the source did confirm, and keep going.
- Keep a glossary of Arabic domain terms → the English term you chose, so the client can check it.
- If an ambiguity blocks the current stage, quote the phrase and ask, in Arabic, which reading is
  intended. If it does not block, record the ambiguity as `Q-xx` and continue.

## Avoiding triplication

The same requirement must not be restated three times in three slightly different ways. Each
document has one job:

| Document | Says |
|----------|------|
| `01-prd.md` | **What the product must do** — confirmed actors, behavior, scope, constraints, and open questions. This is the primary product-requirements document. |
| `brd.md` (optional) | **Why the organization is investing** — only when a business, organizational, or contractual need exists. Not part of the default package. |
| `02-business-rules.md` | **What must always be true**, regardless of UI. References the PRD; does not restate it. |
| `03-use-cases.md` | **How** an actor reaches a goal, step by step |
| `05-srs.md` | **The testable system statement** — EARS, with numbers, traced to the PRD |
| `08-user-stories.md` | **What gets built next** — sliced, estimable, with acceptance criteria |

When you catch yourself repeating a sentence from an earlier document, replace it with the id.
Do not generate `brd.md` by default. A separate BRD is justified only by a real business,
organizational, or contractual need, and it points at the PRD for product behavior.

## MUST DO

- Ask only blocking clarification questions, in Arabic, at most four in one batch. Use
  `AskQuestion` when that tool is available, with Arabic prompts and option labels. If it is not
  available, ask in Arabic chat and wait. Do not invent a tool name or proceed as if the questions
  were answered. Record everything else under Open Questions and continue.
- If the product has no name, use a provisional descriptive name and continue.
- Default scope to MVP unless the user specified otherwise. Do not ask them to confirm that
  default when the source is already a small initial scope.
- **Do not assume a platform when the choice would change the design.** Ask the Arabic platform
  question when a design decision needs it and it is still open. Once answered, do not ask again.
- **Before any color, font, layout, or frame size, the platform must be settled**, and written
  into `13-design-brief.md` §0 with its frame, breakpoints, navigation pattern, and input model.
- Run the **style picker** at 13b before writing the brief's §6, and write the component specs from
  the user's picks with page citations — not invented.
- Report which components the user left unchosen. Never default one silently.
- Record every departure from a picked style in the brief's **Deviations from the style library**
  table, with a reason. Arabic RTL will produce real ones — that is the system working.
- Create a fresh numbered run folder for each run.
- Gate after every stage, with real options written in Arabic. Batch only when the user asks.
- Write documents in English and UI artifacts in Arabic/RTL.
- Give every `NFR-xx` you write a **number** and a measurement method. If the source gives no number, record `Q-xx` and do not invent a target to pass the gate.
- Give every `US-xx` acceptance criteria in Given/When/Then, plus priority and points.
- Give every `BR-xx` a provenance, an enforcement point, and a violation response.
- Give every `FR-xx` an EARS sentence and the `UC-xx` it realizes.
- Ask for existing brand assets before proposing any palette or typography, unless that answer is already recorded.
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
- Do not restate the same requirement across the PRD, SRS, and stories — use the id instead.
- Do not generate a separate BRD by default. Do not rename a product requirement into a business
  requirement just to keep a BRD in the package.
- Do not invent entities, endpoints, statuses, transitions, rules, or requirements the source and
  the PRD do not support. Unsupported additions go under `A-xx` assumptions, or under `Q-xx` when
  the fact is simply unknown, and get flagged. Do not treat a speculative API field or data-model
  value as a final requirement.
- Do not write an untestable rule ("the system should be fast") or an unmeasurable NFR.
- Do not write a story larger than 13 points without splitting it.
- Do not ask the user in English. Do not ask a question the run log already answers. Do not ask
  the user to confirm a low-risk default. Do not ask every possible question at intake.
- Do not assume a platform when that choice would change the design, and do not invent one when
  the user leaves it open.
- Do not propose colors, fonts, layouts, or frame sizes before the platform is settled, and not
  before asking about existing brand when that answer is still unknown.
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
