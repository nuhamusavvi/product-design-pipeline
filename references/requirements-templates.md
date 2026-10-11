# Requirements Templates — Documents 01 to 04

All four documents are written in **English**. Arabic appears only in the glossary (01) and in
quoted source phrases, always marked as such.

Ids are permanent once written. Never renumber mid-run. See the ID registry in `SKILL.md`.

**The division of labour across the package** — keep it clean or the same requirement ends up
stated three times in three slightly different ways:

| Document | Answers |
|----------|---------|
| `01-prd.md` | **What the product must do** — confirmed actors, behavior, scope, constraints, and open questions. Primary product-requirements document. |
| `brd.md` (optional, not a stage) | **Why the organization is investing** — only when a business, organizational, or contractual need exists |
| `02-business-rules.md` | **What must always be true**, regardless of UI. References the PRD; does not restate it. |
| `03-use-cases.md` | **How** an actor accomplishes a goal, step by step |
| `04-permission-matrix.md` | **Who** may do what, to which data — the detailed matrix. The PRD states only the confirmed product-level permissions. |
| `05-srs.md` | **The testable system statement** — EARS, traced to the PRD. Not a second copy of the PRD. |
| `08-user-stories.md` | **What gets built next** — the sliced backlog. Acceptance criteria are written here, not repeated in the PRD. |

---

## 01 — `01-prd.md` (Product Requirements Document)

Audience: product, design, and engineering. This is the primary reference for product requirements
and behavior. Write it in English. No implementation detail that belongs in the SRS, the data
model, or the API sketch.

Every statement is tagged **Confirmed**, **Assumption `A-xx`**, or **Open `Q-xx`**. A default is
tagged **Default** and is not a confirmed requirement. Do not invent missing rules. The
device-maintenance example in `intake-questions.md` shows what to confirm, what to default, and
what to leave open. Do not copy that example into other products.

Do not generate a separate BRD as part of this stage. See **Optional BRD** below.

```markdown
# Product Requirements Document — <Product Name>

Source: Arabic requirements provided <date>. Run: product-design/NN-slug/
Product name: Confirmed | Provisional
Status: Draft · Approved at gate 1 on <date>

## 1. Executive summary
<Five sentences a reader can use to understand the product: who it is for, what it does, and what
this release includes. Only confirmed behavior here. Point at §8 for what is still open.>

## 2. Problem statement

### The problem today
<2–4 sentences: what is broken, for whom, and what it costs them. If the source did not state the
cost, do not invent one — mark the gap `A-xx` or `Q-xx`.>

### Why now
<Only when the source or the user gave a reason. Otherwise leave this as `Q-xx` and continue.>

## 3. Objectives

| # | Objective | Success measure | Baseline | Target | Status |
|---|-----------|-----------------|----------|--------|--------|
| G-01 | <objective the source supports> | <measure> | <baseline or "not stated"> | <target or "not stated"> | Confirmed |

Objectives without a measure are aspirations, not objectives. If the source gives no number, do
not invent one. Record `Q-xx` or, when a placeholder is useful and low-risk, `A-xx`.

### Non-goals
- <what the source or the MVP default puts out of scope, and why>

## 4. Actors and roles

### P-01 — <Role name>
- **Status**: Confirmed | Assumption
- **Who**: what the source says. Unknown demographics stay blank or `Q-xx`. Do not invent age,
  device tier, or tech comfort.
- **Goal**: what they come to the product to accomplish
- **Confirmed behavior**: what this role can do, in the source's words
- **Success looks like**: only if the source or a later answer says so

<repeat per persona the source supports>

Detailed capabilities live in `04-permission-matrix.md`. Do not copy that matrix here.

## 5. Scope

Default the release to **MVP** unless the user specified otherwise. Tag that choice **Default**
when the user did not say it.

### In scope
- <one confirmed capability per line>

### Out of scope (this phase)
| Item | Reason | Status | Revisit when |
|------|--------|--------|--------------|

### Release phasing
| Phase | Contents | Status | Rationale |
|-------|----------|--------|-----------|
| MVP | | Default or Confirmed | |
| Later | | Open, if the source never described it | |

## 6. Non-functional summary
One line per category the source or a documented default actually supports — performance,
availability, security, privacy, accessibility, localization, scale. Tag each line. **Measurable
targets live in `05-srs.md` §NFR.** Do not duplicate the numbers, and do not invent a target to
fill a row. A missing target is `Q-xx`.

## 7. Assumptions

| # | Assumption | Basis | Impact if wrong | Owner |
|---|-----------|-------|-----------------|-------|
| A-01 | <something added so the product is coherent, not stated by the source> | <why it was assumed> | <what breaks> | Client |

An assumption is not a confirmed requirement.

## 8. Open questions

| # | Question | Blocking? | Owner | Needed by |
|---|----------|:---------:|-------|-----------|
| Q-01 | <unknown statuses, platform, or other gap> | No | Client | Stage 10 |

A **No** in Blocking means the workflow continues. Do not stop to ask it. Ask later, in Arabic,
only when a stage cannot proceed without the answer.

## 9. Constraints and dependencies
Product constraints the source or the user actually stated: deadline, existing systems,
regulation, third-party availability. Unknown constraints are `Q-xx`, not invented limits.

## 10. Glossary — Arabic source terms

| Arabic term | English term used | Notes |
|-------------|-------------------|-------|
| <source term> | <English term used in these documents> | |

## 11. Related documents

| Document | What it contains |
|----------|------------------|
| `02-business-rules.md` | Rules and decision logic. References this PRD; does not restate it. |
| `03-use-cases.md` | How an actor reaches a goal |
| `04-permission-matrix.md` | Who may do what, and to whose data |
| `05-srs.md` | Testable functional and non-functional requirements, traced here |
| `08-user-stories.md` | The sliced backlog and the acceptance criteria |
| `brd.md` | Present only when a separate business-requirements document was justified |

## 12. Confirmed product behavior

One behavior per line, tagged **Confirmed**. This is the functional behavior the source
supports. Later `FR-xx` items in `05-srs.md` trace to these lines. Do not restate them there in
different words.

- <confirmed behavior> — Confirmed

Unknown behavior, including unnamed statuses and transitions, is not listed here. It is `Q-xx`
in §8.

## 13. Permissions and expected system behavior

Product-level summary only, for roles §4 already confirmed.

| Actor | Confirmed expectation | Status |
|-------|----------------------|--------|
| <role> | <what the source says they can see or do> | Confirmed |

The permission matrix is the detailed form. Do not invent cells the source did not support.

## 14. Acceptance criteria

List only criteria the source already stated, each tagged **Confirmed**. Given/When/Then
criteria are written once, in `08-user-stories.md`, and traced back here. Do not copy them into
this section.
```

**Quality bar**: every confirmed sentence of the Arabic source maps to an objective, a scope
line, a confirmed behavior, a rule in 02, a use case in 03, an out-of-scope row, or an open
question. Nothing silently dropped. Nothing invented and labeled Confirmed.

### Optional BRD — do not generate by default

Write `brd.md` in the run folder only when there is a genuine business, organizational, or
contractual need: a sponsor needs a business case, a contract separates business obligations
from product behavior, or governance requires a business-requirements document. It is not a
pipeline stage and it does not replace `01-prd.md`.

When it is justified, `brd.md` states the business problem, organizational objectives, and
contractual or organizational constraints, in English, and points to `01-prd.md` for actors,
product behavior, permissions, and acceptance criteria. Do not copy those into the BRD.

If that need does not exist, do not create the file, do not add a stage, and do not add a page
for it in `docs-html/`.

---

## 02 — `02-business-rules.md`

Audience: product, QA, and the backend team. These are the invariants — true regardless of which
screen the user is on, or whether there is a UI at all.

Reference the relevant PRD behavior instead of restating it. Do not invent a rule, a status
name, or a transition the source did not give. If statuses are missing, leave the lifecycle
section empty, point at the `Q-xx` in `01-prd.md` §8, and document only the confirmed behavior.
The sample rows below show the table format. Do not copy them into a run.

````markdown
# Business Rules — <Product Name>

A rule belongs here if it is true independently of the interface. "The cancel button is disabled"
is not a rule; "a booking may not be cancelled within 24 hours of its start" is.

## Index

| Category | Count |
|----------|------:|
| Validation | |
| Calculation | |
| Authorization | |
| Lifecycle | |
| Temporal | |
| Data integrity | |

## Rules

| # | Rule | Category | Applies to | Enforced at | Provenance | Violation response |
|---|------|----------|-----------|-------------|------------|--------------------|
| BR-01 | A booking may not be cancelled less than 24 hours before its start time. | Temporal | UC-04, FR-12 | Server | Arabic source ¶3 | Reject with a message offering reschedule |
| BR-02 | A phone number must be unique across active accounts. | Data integrity | UC-01, FR-03 | Both | Assumption A-04 | Inline field error, offer sign-in |

**Column rules**
- **Rule** — one testable sentence. A tester must be able to say pass or fail. No "should be fast",
  no "user-friendly".
- **Category** — validation · calculation · authorization · lifecycle · temporal · data integrity.
- **Applies to** — the `UC-xx` and `FR-xx` this constrains. Filled for `UC-xx` at stage 3 and
  completed with `FR-xx` at stage 5.
- **Enforced at** — `Client` · `Server` · `Both`. Client-only is almost always a defect; say why
  if you write it.
- **Provenance** — a quoted phrase or paragraph reference from the Arabic source, or `Assumption
  A-xx`. Every rule has one.
- **Violation response** — what the system does when the rule is broken. This is what stage 11
  turns into an error state and stage 12 turns into a negative test.

## Calculations
Rules involving arithmetic get their own section with the formula written out, worked examples,
rounding policy, and currency/precision handling.

### BR-07 — Booking fee
```
fee = base_rate × duration_hours × (1 - discount_rate)
rounded to 2 decimals, half-up
```
| base_rate | duration | discount | fee |
|-----------|----------|----------|-----|
| 120.00 | 1.5 | 0.10 | 162.00 |

## Lifecycle rules
State machines, one per entity that has one. Table of from-state → event → to-state → guard rule.
Cross-reference the state-transition permissions in `04-permission-matrix.md`.

## Rules deferred or rejected
| Rule considered | Why not now |
|-----------------|-------------|
````

---

## 03 — `03-use-cases.md`

Audience: BA, product, and whoever writes the flows. One use case per user goal, not per screen.
Trace each use case to a confirmed PRD behavior or objective. A step the source did not describe
is an assumption, not a confirmed requirement. Do not invent status transitions; point at the
open question in `01-prd.md` §8.

```markdown
# Use Cases — <Product Name>

## Index

| # | Use case | Actor | Priority | Objective | Realized by |
|---|----------|-------|----------|-----------|-------------|
| UC-01 | Register and verify account | Guest | Must | G-01 | F-01 |

## Actor × use case grid

| Use case | Guest | Customer | Provider | Admin |
|----------|:-----:|:--------:|:--------:|:-----:|
| UC-01 | ● | | | |
| UC-04 | | ● | ● | ● |

● = primary actor · ○ = secondary/participating actor

---

## UC-01 — <Verb phrase, e.g. "Book an appointment">

- **Primary actor**: P-01 Customer
- **Secondary actors**: payment gateway, SMS provider
- **Goal**: <one sentence, from the actor's point of view>
- **Trigger**: <what starts it>
- **Frequency**: <how often, per user — drives how much polish the flow needs>
- **Preconditions**:
  - <what must already be true>
- **Guarantees**
  - *Minimal* (even on failure): <e.g. no charge is made>
  - *Success*: <e.g. a confirmed booking exists and the user has been notified>

### Main flow
1. Actor does X.
2. System validates against BR-03.
3. …

### Alternate flows
- **UC-01.a — <condition>**: at step 3, if <condition>, then <steps>, rejoining at step 5.

### Failure paths
| Step | What goes wrong | System response | Rule |
|------|-----------------|-----------------|------|
| 4 | Payment declined | Keep the booking held for 10 min, offer another method | BR-09 |

### Postconditions
<what is true afterwards, in the data>

### Related
- **Rules**: BR-03, BR-09
- **Flow**: F-01
- **Screens**: filled at stage 10
- **Requirements**: filled at stage 5

<repeat for every use case, numbered UC-01 upward, grouped by actor>

## Coverage check
Every objective `G-xx` in `01-prd.md` is realized by at least one use case. Every use case traces
to an objective. List any that does not and say why it stays.
```

**Quality bar**: every use case has at least one failure path. A failure path the source does not
support is an assumption, tagged as such, not a confirmed rule. A use case with only a happy path
is unfinished and will produce an incomplete flow at stage 9 and a thin backlog at stage 8.

---

## 04 — `04-permission-matrix.md`

Audience: backend and security. This is the document that stops "can a customer see another
customer's phone number?" from being answered in a code review.

Roles and capabilities must match the confirmed actors in `01-prd.md`. Do not invent a
permission the source did not support; record `Q-xx` instead. The sample matrix below is a
format illustration. Do not copy it into a run.

```markdown
# Permission Matrix — <Product Name>

## Roles

| Role | Description | How it is granted | Count estimate |
|------|-------------|-------------------|----------------|
| Guest | Unauthenticated visitor | Default | — |
| Customer | Verified account holder | Phone OTP verification | Many |
| Provider | Service provider | Admin approval after document check | Tens |
| Admin | Back-office operator | Assigned internally | Few |

Roles are additive or exclusive — say which. If a user can hold two roles at once, state how
conflicts resolve.

## Capability matrix

| Capability | Guest | Customer | Provider | Admin | Rule |
|------------|:-----:|:--------:|:--------:|:-----:|------|
| Browse catalog | ✅ | ✅ | ✅ | ✅ | — |
| Place booking | ❌ | ✅ | ❌ | ⚠️¹ | BR-05 |
| Cancel own booking | ❌ | ⚠️² | ⚠️² | ✅ | BR-01 |
| View customer phone | ❌ | ❌ | ⚠️³ | ✅ | BR-14 |
| Approve provider | ❌ | ❌ | ❌ | ✅ | BR-21 |

✅ allowed · ❌ denied · ⚠️ conditional — every ⚠️ carries a numbered footnote:

1. Admin may place a booking on behalf of a customer; the audit log records both identities.
2. Only outside the 24-hour window (BR-01).
3. Only for a booking assigned to that provider, and only after it is confirmed.

Group capabilities by module so the table stays readable. Every capability that any screen or
endpoint exposes must appear here — completeness is checked against `07-api-surface.md` at stage 16.

## Data scope

Beyond "may they call it", define "over which rows".

| Role | Entity | Scope | Filter |
|------|--------|-------|--------|
| Customer | Booking | Own | `booking.customer_id = current_user.id` |
| Provider | Booking | Assigned | `booking.provider_id = current_user.id` |
| Admin | Booking | All | — |

## Field-level restrictions

| Entity | Field | Visible to | Editable by | Rule |
|--------|-------|-----------|-------------|------|
| Customer | phone | Self, Admin, assigned Provider after confirmation | Self, Admin | BR-14 |
| Booking | internal_notes | Admin | Admin | — |

## State transition permissions

Who may move an entity from one state to another. Pair this with the lifecycle rules in
`02-business-rules.md`.

| Entity | From | To | Guest | Customer | Provider | Admin | Guard |
|--------|------|----|:-----:|:--------:|:--------:|:-----:|-------|
| Booking | pending | confirmed | ❌ | ❌ | ✅ | ✅ | BR-06 |
| Booking | confirmed | cancelled | ❌ | ⚠️ | ✅ | ✅ | BR-01 |

## Escalation and delegation
Can a role act on behalf of another? Is there impersonation for support? What is audited?

## Unauthenticated surface
Everything reachable without a session, listed explicitly. This is the attack surface —
the security reviewer reads this section first.

## Defaults
- Deny by default. A capability absent from this matrix is denied.
- Every permission decision is enforced server-side. Client-side checks are UX, not security.
```

**Quality bar**: no `⚠️` without a footnote; every role has a data-scope row for every entity it can
reach; the unauthenticated surface section is never empty (it at least lists the splash and
auth screens).
