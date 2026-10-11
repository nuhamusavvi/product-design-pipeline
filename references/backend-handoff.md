# Stage 10 — Consolidated Backend Handoff

Write `product-design/NN-slug/03-backend-handoff-en.md` only after every non-blocked screen has
an English prompt. This is the last stage.

One English Markdown document. Do not split it, and do not write an Arabic copy. Do not paste
the Lovable prompts into it. Do not generate HTML.

Read `00-analysis-ar.md`. Keep every `FR-xx`, `BR-xx`, `P-xx`, `W-xx`, `F-xx`, `SC-xx`, `Q-xx`,
and `A-xx`. Keep Plane task identifiers unchanged. Do not describe a task marked unread.

## Rules

- Confirmed means the retrieved source or a recorded answer supports it.
- An assumption is labeled and is not a requirement.
- Do not invent API paths, HTTP methods, database tables, columns, enums, authentication,
  authorization mechanisms, technology choices, infrastructure, or integrations.
- If the UI needs information, name the information and the `SC-xx`. Leave storage and transport
  as backend decisions.
- Omit a section that the source does not support, and write "None confirmed." Do not fill it
  with a typical design.

## Document

```markdown
# Backend Handoff — <Product Name>

- Run folder: product-design/NN-slug/
- Product name: Confirmed | Provisional
- Scope: MVP (default) | as specified by the user
- Interface language and direction: as recorded in the analysis, or unresolved
- Status: Draft <date>

## 1. Project Overview

<Confirmed product, users, and this scope. Point to section 13 for open items.>

## 2. Scope

### In scope

- FR-01 — <capability>

### Out of scope

- <Only exclusions the source stated, or items left out because they were never requested under the MVP default. Do not drop a stated requirement.>

## 3. Functional Requirements

| ID | Requirement | Status | Screens | Source tasks |
|----|-------------|--------|---------|--------------|
| FR-01 | | Confirmed | SC-01 | |

## 4. Actors and Permissions

| ID | Actor | Confirmed actions | Restricted only if stated | Not specified |
|----|-------|-------------------|---------------------------|---------------|
| P-01 | | | | Q-xx |

How access is enforced is not decided here unless the source named a mechanism.

## 5. Business Rules

| ID | Rule | Status | Related requirements | Source tasks |
|----|------|--------|----------------------|--------------|
| BR-01 | | Confirmed | FR-01 | |

If the source stated no rule, write "None confirmed."

## 6. Business Workflows

### W-01 — <Name>

- Actor: P-0x
- Trigger:
- Preconditions:
- Result:
- Unresolved: Q-xx

1.
2.

## 7. Screen-to-Backend Requirements

### SC-01 — <Screen name>

- Actor: P-0x
- Actions that need backend support:
- Information the screen displays:
- Information the user submits:
- Journey: F-0x
- Unresolved behavior: Q-xx

<Repeat for each non-blocked screen. For a blocked screen, name the ID and the missing decision.>

## 8. Data Requirements Supported by the Source

Not a schema.

| Information | Why it is needed | Supported by | Open point |
|-------------|------------------|--------------|------------|
| | | FR-xx, SC-01 | Q-xx or none |

## 9. Validation and State-Transition Rules

| Situation | Confirmed behavior | Screen | Not specified |
|-----------|--------------------|--------|---------------|
| | | SC-01 | |

Do not invent status names, transitions, or error codes.

## 10. External Integrations Explicitly Mentioned

None confirmed, unless the source named a system. Do not add one.

## 11. Notifications and Background Processes

Include this section only when the source requires a notification or a background process.
Otherwise write "None confirmed."

## 12. Error and Exception Handling Requirements

User-facing failure behavior the source or the UI states support. Do not invent codes.

## 13. Open Questions

| ID | Question | What it affects |
|----|----------|-----------------|
| Q-01 | | SC-01 |

## 14. Assumptions and Unconfirmed Decisions

| ID | Assumption or decision | Why it is not confirmed |
|----|------------------------|-------------------------|
| A-01 | | |

### Left to the backend team

- Storage representation
- API shape and transport
- Authentication and session mechanism, if still unspecified

## 15. Traceability to Source Tasks

| Requirement | Rule | Workflow | Journey | Screens | Source tasks |
|-------------|------|----------|---------|---------|--------------|
| FR-01 | BR-01 or — | W-01 | F-01 | SC-01 | Plane ids, or — |

Every `FR-xx` appears once. Every non-blocked `SC-xx` appears once. List any ID without a home
under **Unresolved traceability**. If that list is empty, write "None."
```

Use the run's real IDs. Delete placeholder rows that this product does not have.
