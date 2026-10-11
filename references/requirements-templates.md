# Requirements Templates — Documents 01 to 04

All four documents are written in **English**. Arabic appears only in the glossary (01) and in
quoted source phrases, always marked as such.

Ids are permanent once written. Never renumber mid-run. See the ID registry in `SKILL.md`.

**The division of labour across the package** — keep it clean or the same requirement ends up
stated three times in three slightly different ways:

| Document | Answers |
|----------|---------|
| `01-brd.md` | **Why** are we building this, for whom, and what is in scope |
| `02-business-rules.md` | **What must always be true** about the business, regardless of UI |
| `03-use-cases.md` | **How** an actor accomplishes a goal, step by step |
| `04-permission-matrix.md` | **Who** may do what, to which data |
| `05-srs.md` | **What the system does** — the buildable specification |
| `08-user-stories.md` | **What gets built next** — the sliced, estimable backlog |

---

## 01 — `01-brd.md` (Business Requirements Document)

Audience: the client and the product owner. Business language, no implementation detail.

```markdown
# Business Requirements Document — <Product Name>

Source: Arabic requirements provided <date>. Run: product-design/NN-slug/
Status: Draft · Approved at gate 1 on <date>

## 1. Executive summary
<Five sentences a stakeholder can read and understand the whole product from.>

## 2. Problem statement

### The problem today
<2–4 sentences: what is broken, for whom, and what it costs them.>

### Why now
<What makes this the moment — a deadline, a competitor, a regulation, a cost.>

## 3. Objectives

| # | Objective | Success measure | Baseline | Target |
|---|-----------|-----------------|----------|--------|
| G-01 | Reduce booking time | Median minutes from open to confirmed | 6 min (phone) | < 90 s |

Objectives without a measure are aspirations, not objectives. If the source gives no number,
propose one and flag it as `A-xx`.

### Non-goals
- <what this product deliberately does not try to do, and why>

## 4. Users

### P-01 — <Role name>
- **Who**: age range, context, tech comfort, device tier
- **Goal**: what they come to the product to accomplish
- **Frustrations today**: what makes the current process painful
- **Success looks like**: the moment they feel the product worked
- **Volume**: rough share of total users

<repeat per persona>

Full role capabilities live in `04-permission-matrix.md`.

## 5. Scope

### In scope
- <bulleted, concrete, one capability per line>

### Out of scope (this phase)
| Item | Reason | Revisit when |
|------|--------|--------------|

### Release phasing
| Phase | Contents | Rationale |
|-------|----------|-----------|
| MVP | | |
| Phase 2 | | |

## 6. Non-functional summary
One line per category — performance, availability, security, privacy, accessibility, localization,
scale. **The measurable targets live in `05-srs.md` §NFR.** This section is the business-readable
summary only; do not duplicate the numbers.

## 7. Assumptions

| # | Assumption | Basis | Impact if wrong | Owner |
|---|-----------|-------|-----------------|-------|
| A-01 | Users have smartphones with data | Market norm | Whole product model | Client |

## 8. Open questions

| # | Question | Blocking? | Owner | Needed by |
|---|----------|:---------:|-------|-----------|
| Q-01 | | Yes/No | Client | Stage 5 |

## 9. Constraints and dependencies
Budget, deadline, existing systems, regulatory, third-party availability.

## 10. Glossary — Arabic source terms

| Arabic term | English term used | Notes |
|-------------|-------------------|-------|
| حجز | Booking | Not "reservation" — used for appointments throughout |

## 11. Related documents

| Document | What it contains |
|----------|------------------|
| `02-business-rules.md` | The <n> rules that constrain how the business operates — <one line> |
| `03-use-cases.md` | The <n> use cases that realize the objectives above — <one line> |
| `04-permission-matrix.md` | Who may do what, and to whose data — <one line> |
| `05-srs.md` | The buildable system specification |
| `08-user-stories.md` | The sliced backlog |
```

**Quality bar**: every sentence of the Arabic source maps to an objective, a scope line, a rule
in 02, a use case in 03, or an explicit out-of-scope row. Nothing silently dropped.

---

## 02 — `02-business-rules.md`

Audience: product, QA, and the backend team. These are the invariants — true regardless of which
screen the user is on, or whether there is a UI at all.

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
Every objective `G-xx` in `01-brd.md` is realized by at least one use case. Every use case traces
to an objective. List any that does not and say why it stays.
```

**Quality bar**: every use case has at least one failure path. A use case with only a happy path
is unfinished and will produce an incomplete flow at stage 9 and a thin backlog at stage 8.

---

## 04 — `04-permission-matrix.md`

Audience: backend and security. This is the document that stops "can a customer see another
customer's phone number?" from being answered in a code review.

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
