# Backlog, QA, and Traceability Templates — Documents 08, 12, 16

The delivery half of the package: what gets built next, how it will be proved, and the matrix that
shows nothing fell through.

Written in **English**.

**Load `../feature-forge/references/acceptance-criteria.md`** before writing documents 08 and 12
— it holds the Given/When/Then formats by scenario type (happy path, error, edge, authorization,
concurrency) and the INVEST table. Do not restate them here.

---

## 08 — `08-user-stories.md`

Audience: the product owner and the delivery team. This is the backlog they will actually plan
sprints from.

````markdown
# User Stories — <Product Name>

Derived from `03-use-cases.md` and `05-srs.md`. Every story implements at least one `FR-xx`;
every `FR-xx` is implemented by at least one story. Gaps are listed in §6.

## 1. Summary

| Epic | Stories | Points | Must | Should | Could |
|------|--------:|-------:|-----:|-------:|------:|
| EP-01 Account & access | 7 | 24 | 5 | 2 | 0 |
| **Total** | **41** | **168** | **26** | **11** | **4** |

## 2. Epics

### EP-01 — Account and access
**Goal**: a new user can create a verified account and sign back in reliably.
**Realizes**: UC-01, UC-02 · **Screens**: S-01…S-06 · **Points**: 24

<repeat per epic — one epic per coherent capability, roughly one to three sprints of work>

## 3. Stories

### US-03 — Verify phone with OTP
> **As a** guest,
> **I want** to confirm my phone number with a code sent by SMS,
> **so that** my account is verified and I can book.

| | |
|---|---|
| **Epic** | EP-01 |
| **Priority** | Must |
| **Points** | 3 |
| **Implements** | FR-01, FR-02, FR-03 |
| **Enforces** | BR-03, BR-04 |
| **Screens** | S-04 (OTP entry), S-05 (locked) |
| **Endpoints** | API-02, API-03 |
| **Depends on** | US-02 |
| **Blocks** | US-04, US-11 |

**Acceptance criteria**

- **AC-01 — Correct code**
  Given a pending account that was sent an OTP less than 5 minutes ago,
  When the guest submits the correct 6 digits,
  Then the account becomes active,
  And the guest lands on the home screen,
  And a session is created.

- **AC-02 — Wrong code**
  Given a pending account,
  When the guest submits an incorrect code,
  Then an inline Arabic error is shown beneath the field,
  And the field is cleared and refocused,
  And the attempt counter increments.

- **AC-03 — Expired code**
  Given an OTP older than 5 minutes,
  When the guest submits it,
  Then an expiry message is shown with a resend action,
  And no session is created.

- **AC-04 — Lockout**
  Given 5 failed attempts within 15 minutes,
  When the guest submits any code,
  Then attempts are refused for 30 minutes,
  And the remaining wait is shown.

**Notes / out of scope**: WhatsApp delivery is Phase 2 (see `01-brd.md` §5).

<repeat per story>

## 4. Story writing rules

- One story = one user-visible outcome, deliverable within a sprint. If it needs more, split by
  workflow step, by role, by happy-path-then-edge-cases, or by CRUD operation — never by layer
  ("backend story" + "frontend story" is not a user story).
- Acceptance criteria are Given/When/Then and testable. Cover the happy path, at least one error
  case, and any authorization rule that applies. Formats and scenario types:
  `../feature-forge/references/acceptance-criteria.md`.
- Check every story against INVEST before writing points.
- Points are Fibonacci (1, 2, 3, 5, 8, 13). A 13 is a warning — split it.
- Technical work that delivers no user-visible outcome is an **enabler**, written as
  `US-xx (enabler)` with a plain description instead of the As-a form, and still pointed.

## 5. Release slicing

| Release | Epics | Stories | Points | Delivers | Cut line rationale |
|---------|-------|--------:|-------:|----------|--------------------|
| MVP | EP-01…EP-04 | 26 | 98 | A customer can register, search, book, and pay | Matches `01-brd.md` §5 |

## 6. Coverage and gaps

| Check | Result |
|-------|--------|
| `FR-xx` with no story | list, or "none" |
| Story implementing no `FR-xx` | list, or "none" |
| `UC-xx` with no epic | list, or "none" |
| Story touching no screen | list, or "none" |

## 7. Definition of done

A story is done when:
- [ ] All acceptance criteria pass
- [ ] Unit and integration tests written and green
- [ ] The `TC-xx` cases in `12-test-scenarios.md` for this story pass
- [ ] Permissions enforced server-side per `04-permission-matrix.md`
- [ ] Arabic copy matches `14-wireframes.md`; RTL layout verified against `15-ui-designs/`
- [ ] Empty, loading, and error states implemented per `11-states-and-edge-cases.md`
- [ ] Accessibility spot-check: focus order, contrast, touch targets, screen-reader labels
- [ ] No new physical CSS directions (`left`/`right`) — logical properties only
- [ ] Reviewed and merged; documentation updated if the contract changed
````

---

## 12 — `12-test-scenarios.md`

Audience: QA. Written after screens and states exist so every case names where it runs.

````markdown
# Test Scenarios — <Product Name>

Derived from the acceptance criteria in `08-user-stories.md`, the states in
`11-states-and-edge-cases.md`, the rules in `02-business-rules.md`, and the permission matrix in
`04-permission-matrix.md`.

## 1. Summary

| Type | Count | Must-pass |
|------|------:|----------:|
| Functional | | |
| Negative | | |
| Authorization | | |
| Edge case | | |
| Integration | | |
| Accessibility | | |
| Localization / RTL | | |
| **Total** | | |

## 2. Test cases

### TC-014 — OTP lockout after five failures
| | |
|---|---|
| **Type** | Negative |
| **Priority** | High |
| **Verifies** | US-03/AC-04, FR-03, BR-04 |
| **Screen** | S-04 |
| **Preconditions** | A pending account exists; no prior failed attempts in the window |

**Steps**
1. Submit an incorrect OTP. → Inline error, counter = 1.
2. Repeat four more times. → Counter = 5.
3. Submit any code, correct or not.

**Expected**
Attempt is refused without validating the code. A lockout message states the remaining wait in
Arabic. No session is created. The counter resets 30 minutes after the fifth failure.

**Data**: phone `+9665xxxxxxxx`, codes `000000` ×5

<repeat per test case>

## 3. Coverage matrix

Screens down, test types across. Empty cells are the finding — they show where QA has no coverage.

| Screen | Functional | Negative | Authz | Edge | A11y | RTL |
|--------|:----------:|:--------:|:-----:|:----:|:----:|:---:|
| S-04 OTP entry | TC-012 | TC-013, TC-014 | — | TC-015 | TC-088 | TC-101 |

## 4. Authorization test set

One case per `⚠️` and per denied cell in `04-permission-matrix.md` that a user could plausibly
attempt. Each verifies **server-side** enforcement, not just a hidden button — attempt the call
directly with the wrong role and assert the rejection.

| # | Role | Attempts | Expected | Matrix row |
|---|------|----------|----------|------------|
| TC-060 | Customer | Cancel another customer's booking | 403, no state change | Cancel own booking |

## 5. Arabic and RTL test set

Not optional, and not covered by the functional cases. At minimum:

| # | Check | Where | Expected |
|---|-------|-------|----------|
| TC-101 | Mixed Arabic + Latin + digits in one line | Any screen showing prices or brands | No reversed runs; `<bdi>` isolation holds |
| TC-102 | Long Arabic name overflow | Profile, list rows, headers | Clamps to the specified line count, no layout break |
| TC-103 | Digit convention consistency | Every numeric surface | Matches the run-log choice everywhere, including badges |
| TC-104 | Date and calendar rendering | Bookings, history | Matches the stage-0 calendar choice; Arabic weekday names |
| TC-105 | Directional icon mirroring | Back, chevrons, progress, send | Mirrored; clocks and media controls not mirrored |
| TC-106 | Layout direction | Every screen | `dir="rtl"`; back affordance at inline-start; tab order right-to-left |
| TC-107 | Text input caret and alignment | Every form field | Caret starts at the right; `text-align: start` |
| TC-108 | Currency placement and format | Prices, totals, invoices | Per `13-design-brief.md` §7 |

## 6. Accessibility test set
Keyboard-only traversal of each flow, focus-visible on every control, contrast spot-checks against
`13-design-brief.md` §4, screen-reader labels on icon-only controls, 200% text scaling, and
`prefers-reduced-motion`.

## 7. Integration test set
One case per external system in `05-srs.md` §6, covering the success path, the timeout path, and
the "provider is down" path. Payment gets an explicit double-charge test (E-02).

## 8. Regression candidates
Cases that must run on every release, marked from the set above.

## 9. Untested by design
Anything deliberately not covered, with the reason. An honest empty-coverage list beats a matrix
padded with cases nobody will run.
````

---

## 16 — `16-traceability-matrix.md`

Audience: everyone. This is the document that proves the package is coherent. It is generated by
reading the other documents, not by memory.

````markdown
# Traceability Matrix — <Product Name>

Generated at stage 16 by reading documents 01–15. Every cell is verified, not asserted.

## 1. Chains

```
BR-xx  →  FR-xx  →  US-xx  →  S-xx  →  TC-xx      business rule to test
UC-xx  →  F-xx   →  S-xx                          use case to screen
FR-xx  →  API-xx →  EN-xx                         requirement to data
G-xx   →  UC-xx                                   objective to use case
```

## 2. Requirement traceability

| BR | FR | US | Screens | Endpoints | Tests | Status |
|----|----|----|---------|-----------|-------|:------:|
| BR-01 | FR-18 | US-14 | S-22, S-23 | API-15 | TC-041, TC-042 | ✅ |
| BR-04 | FR-03 | US-03 | S-04, S-05 | API-03 | TC-014 | ✅ |
| BR-11 | FR-27 | — | S-31 | API-22 | — | ⚠️ no story, no test |

## 3. Use case traceability

| UC | Objective | Flow | Screens | Stories | Status |
|----|-----------|------|---------|---------|:------:|
| UC-01 | G-01 | F-01 | S-01…S-06 | US-01…US-05 | ✅ |

## 4. Screen traceability

| Screen | Flow | Stories | States defined | Wireframe | UI file | Tests | Status |
|--------|------|---------|:--------------:|:---------:|:-------:|-------|:------:|
| S-04 | F-01 | US-03 | 5 | ✅ | ✅ | TC-012…015 | ✅ |

## 5. Gap report

**Report every gap, in both directions. An empty gap report is a valid result — say so explicitly
rather than omitting the section.**

| # | Gap | Type | Where | Recommendation |
|---|-----|------|-------|----------------|
| GAP-01 | BR-11 has no functional requirement | Orphan rule | `02` → `05` | Add an FR or move BR-11 out of scope |
| GAP-02 | S-31 has no test case | Untested screen | `10` → `12` | Add at least a functional and an error case |

Gap types to check, each in both directions:

| Check | Direction |
|-------|-----------|
| Objective with no use case / use case serving no objective | `01` ↔ `03` |
| Business rule with no requirement / requirement enforcing nothing | `02` ↔ `05` |
| Use case with no flow / flow realizing no use case | `03` ↔ `09` |
| Capability with no endpoint / endpoint with no matrix permission | `04` ↔ `07` |
| Requirement with no story / story implementing nothing | `05` ↔ `08` |
| Entity with no endpoint / endpoint referencing a missing entity | `06` ↔ `07` |
| Flow step landing on no screen / screen in no flow | `09` ↔ `10` |
| Screen with no wireframe / wireframe with no screen | `10` ↔ `14` |
| Screen with no UI file / UI file with no screen | `10` ↔ `15` |
| Acceptance criterion with no test / test verifying nothing | `08` ↔ `12` |
| Screen with no test coverage | `10` ↔ `12` |
| Edge case with no test | `11` ↔ `12` |

## 6. Handoff readiness

| Dimension | Check | Result |
|-----------|-------|--------|
| Complete | Every deliverable present and approved | ✅ 17/17 |
| Traceable | No orphans in either direction | ⚠️ 2 gaps, listed above |
| Testable | Every story has acceptance criteria; every screen has a test | ✅ |
| Buildable | Data model and API cover every requirement | ✅ |
| Specified | Every NFR carries a number | ✅ |
| Secure | Every capability enforced server-side and tested | ✅ |
| Localized | RTL and Arabic test set present and passing | ✅ |

## 7. Counts

| Artifact | Count |
|----------|------:|
| Objectives · Personas | |
| Business rules · Use cases | |
| Functional · Non-functional requirements | |
| Entities · Endpoints | |
| Epics · Stories · Points | |
| Flows · Screens · Edge cases | |
| Test cases | |

These are the numbers the stage-17 dashboard renders. Compute them here, once.
````

---

## `README.md` — the handoff index

Written at stage 16 alongside the matrix, at the root of the run folder. The front door for whoever
receives the package.

````markdown
# <Product Name> — Product & Design Package

Generated <date> from Arabic requirements. Run `product-design/NN-slug/`.

**Start here**: open `docs-html/index.html` in a browser for the interactive version of everything
below. No server, no build step.

## Deliverables

| # | Document | Answers | Primary owner |
|---|----------|---------|---------------|
| 01 | `01-brd.md` | Why are we building this, for whom, what is in scope | Product |
| 02 | `02-business-rules.md` | What must always be true | Product + QA |
| 03 | `03-use-cases.md` | How does an actor reach a goal | BA |
| 04 | `04-permission-matrix.md` | Who may do what, to which data | Backend + security |
| 05 | `05-srs.md` | What does the system do, to what standard | Tech lead |
| 06 | `06-data-model.md` | What is stored and how it relates | Backend |
| 07 | `07-api-surface.md` | What the contract between client and server looks like | Backend + frontend |
| 08 | `08-user-stories.md` | What gets built, in what order | Product owner |
| 09 | `09-user-flows.md` | What path does a user take | UX |
| 10 | `10-screen-list.md` | What screens exist | UX + frontend |
| 11 | `11-states-and-edge-cases.md` | What does each screen do when things go wrong | Frontend + QA |
| 12 | `12-test-scenarios.md` | How will we know it works | QA |
| 13 | `13-design-brief.md` | What does it look like, and why | Design |
| 14 | `14-wireframes.md` | Where does everything sit on each screen | Design + frontend |
| 15 | `15-ui-designs/` | The screens themselves, Arabic and RTL | Frontend |
| 16 | `16-traceability-matrix.md` | Does it all hang together | Everyone |

## Reading order by role

- **Backend**: 05 → 06 → 07 → 04 → 02
- **Frontend**: 10 → 11 → 14 → 15 → 13 → 07
- **QA**: 02 → 08 → 11 → 12 → 04
- **Product owner**: 01 → 03 → 08 → 16
- **Client sign-off**: 01 → 09 → 15

## Conventions

- Documents are English. The product UI is Arabic, right-to-left.
- Ids are stable: `G` objective · `P` persona · `BR` rule · `UC` use case · `FR`/`NFR` requirement ·
  `EN` entity · `API` endpoint · `EP` epic · `US` story · `F` flow · `S` screen · `E` edge case ·
  `TC` test case · `A` assumption · `Q` open question.
- Open questions are collected in `01-brd.md` §8. Assumptions in §7. Both need client answers.

## Status

<paste the handoff readiness table from `16-traceability-matrix.md` §6>

## Known gaps

<paste the gap report from `16-traceability-matrix.md` §5, or state "none">
````
