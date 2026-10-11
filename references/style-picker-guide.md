# Style Picker Guide — Stage 13b

Between confirming the platform (13a) and writing the design brief (13c), the user picks component
styles from a live HTML checklist rendered in the project's own colours and Arabic fonts.

The point: component anatomy — radius scale, dropdown affordance, label placement — has no right
answer, so inventing it per run makes it drift between projects and spends attention on decisions
that don't carry the design. The picker fixes the atoms so the brief can spend itself on the concept.

## The three assets

| File | What it is | Lifetime |
|------|-----------|----------|
| `assets/style-library.html` | The master picker — every component, tiered, with live specimens | Built once from *Design Cheat Sheets* pp.128–242 |
| `assets/style-library-rules.md` | Every extracted rule, tagged `[stated]` or `[inferred]`, cited by page | Read at 13c when writing the brief |

`[stated]` means the book says it. `[inferred]` means it was read off the artwork. On pages like
*Dropdown Styles* (p.176) the six variants carry **no explanatory text at all**, so every description
there is inferred. Treat inferences as reasonable readings, not gospel, and never present one to the
user as though the book asserted it.

---

## Running 13b

### 1. Copy and personalise

Copy `assets/style-library.html` → `<run>/13-style-options.html`, then make exactly three edits:

1. **Swap the `.product-surface` token block** for the project's values — the palette and Arabic
   font families settled at 13a. Every specimen inherits them, so the user sees their own product,
   not a generic one.
2. **Replace `__RUN_SLUG__`** in the script with the run folder slug. This namespaces the
   `localStorage` key: `pdp:01-clinic-booking:styles`.
3. **Bake in prior choices** as `checked` attributes if `13-style-choices.md` already exists —
   see *Re-baking* below.

Nothing else changes. Do not edit the specimens, the citations, or the coherence rules per run.

### 2. Hand it over

Tell the user the absolute path and what to do:

> افتحي `<path>/13-style-options.html` في Chrome أو Edge. اختاري نمطًا لكل مكوّن — تُحفظ اختياراتك
> تلقائيًا، فيمكنك التوقف والعودة لاحقًا. عند الانتهاء اضغطي **حفظ الاختيارات**، ثم أخبريني.

Then **wait**. Do not write the design brief, do not guess the choices, do not proceed to 13c.

### 3. Collect

When the user says they've saved, read `C:\Users\Nuha\Downloads\13-style-choices.md`, move it into
the run folder, and confirm what you got — counts, and specifically what is still unchosen.

The file carries its own progress line:
```
Progress: 14/23 · core 11/13
```

**If it is incomplete, say so precisely.** "You haven't picked a modal, a toast, or a progress
style" — not silence, and not a silent default. The user may deliberately be leaving secondary
components to the defaults; that is fine, but it must be their choice, stated.

### The picker's chrome

The top bar is the page's first element, built after the book's **p.142 #2** mobile top panel —
circled icon buttons, logo at the far inline-end. Right to left: the drawer toggle (**p.150 #2**,
narrow viewports only), the title, then **search**, **fold/unfold all cards**, **save**, and the
logo mark.

- **Search** opens a dialog listing every component card by its Arabic and English name; picking one
  opens that card, scrolls to it, and flashes its header. Enter takes the first result.
- **Fold/unfold** collapses or expands every card at once — the icon reports which action is next.
- Four groups are drawn at laptop scale — **web top panels, pagination, breadcrumb, tabs**.
  Each specimen sits in a scroller pinned to `--specimen-min` (900px), so on a narrow screen it
  keeps its real metrics and scrolls sideways inside its own card rather than being squashed.
  A gradient marks the overflow edge, and it only appears while something is genuinely hidden.
  Card heights and the spacing between components are identical to every other group.
- Progress lives in a **fixed bar at the bottom**: the count, a meter, the unsaved-changes flag, and
  a round button back to the top.
- A group whose choice is made turns **green** in the same tone as the chosen card, so completion is
  visible while scrolling, not only in the side menu.

Tell the user this when handing over the file — none of it is discoverable from a static screenshot.

---

## Storage and the two-session problem

Picking styles across two days is a normal case, not an edge case.

| Concern | Mechanism |
|---|---|
| Stop Monday, resume Thursday | `localStorage`, auto-saved on every change. Reopen and everything is still checked |
| Getting choices to me | The **save icon** in the top bar (`حفظ الاختيارات`) downloads `13-style-choices.md` to Downloads; I read it from there |
| Which is the truth | The **file**. `localStorage` is the fast path; the markdown is the durable record |
| Cleared cache / new machine | Re-bake from the file — see below |

**Namespacing is not optional.** Chrome shares one storage bucket across all `file://` pages, so
without `pdp:<run-slug>:styles` project 2's picker would open showing project 1's choices. This is
silent and confusing when it happens.

**Chrome or Edge only.** Firefox gives each `file://` document a unique opaque origin
(`privacy.file_unique_origin`, default on), so `localStorage` will not persist there. The picker
no longer prints this caveat, so **you must say it when handing the file over.**

### Re-baking

Whenever you touch a run folder that has a `13-style-choices.md`, write those choices back into
`13-style-options.html` as `checked` attributes on the matching radios.

This makes the HTML self-describing on disk: it survives a cleared cache, a different browser, a
different machine, and being emailed to someone else. `localStorage` is a convenience; the file is
the record.

---

## Why the picker is tiered

Roughly 40 component types across the book. A flat list of 40 decisions gets abandoned by the third
project, so the file is built in three tiers:

1. **Foundations** (6) — radius, spacing base, density, elevation, type rhythm, border weight.
   Open by default, chosen first, because they cascade: sharp corners plus an 8px base already rules
   out half the component variants.
2. **Core components** (13) — button, input, dropdown, toggle, chip, card, bottom nav, tabs, toast,
   radio, progress, search, tooltip. Always visible.
3. **Secondary** — collapsed, defaults implied by the tiers above. Opened only if the user cares.

### Coherence warnings

The file flags contradictions live: a pill dropdown beside sharp buttons, a shadowed card under a
"flat" elevation choice, high density with a display type scale. Each is dismissible — sometimes the
contradiction is the design — but it has to be seen and chosen.

This matters more than it looks. Independent picks are each locally sensible and collectively
incoherent; that is the main failure mode of any component catalogue, and the warnings are the guard.

---

## 13c — writing the brief from the choices

Load `assets/style-library-rules.md`, then:

- **§0 Platform and viewport** — already settled at 13a.
- **§3 Visual Style** — from the brand inputs gathered at 13a.
- **§6 UI Direction** — write the component specs **from the picks**, not invented. Pull exact
  metrics from the rules file: button heights 32/40/48/52/56 with their type sizes, input heights
  40/48, dropdown heights 40/48/56, toggle track 40×24, chip 32, and so on. Cite the page for
  anything a developer might question.
- Add what the book omits — the rules file has a *What the book does not cover* section listing
  the gaps: no `focus-visible` anywhere, no RTL guidance, no motion specs, no contrast verification,
  no empty/loading states. Those come from the brief and the pipeline's own standards.

---

## Deviations — what makes "default, not binding" mean something

The picks are **defaults**, not law. Stage 15 may depart from them, but never silently.

`13-design-brief.md` carries a **Deviations from the style library** table:

| Component | Picked | Used instead | Why |
|-----------|--------|--------------|-----|
| Search field | 48px height | 56px | Arabic placeholder wraps at 48 |
| Dropdown | v3 pill | v1 rounded | Pill + 56px height reads as a button, not a select |

Every row is reported at the stage-13 or stage-15 gate. Stage 15's verification checks that anything
in the HTML departing from a picked variant has a row here.

**Arabic RTL is where this will genuinely bite.** The book's metrics assume Latin: a 40px field that
fits an English placeholder often will not fit the Arabic one, and Latin line-heights are too tight
for Arabic. Expect real deviations, record them, and do not treat them as failures — they are the
system working.

---

## Precedence

Three sources can disagree about stage 15. The order is:

1. **`13-design-brief.md` §0 platform profile** — confirmed by the user at a gate. Wins over
   everything, including the book's own "design at 1440 as base" breakpoint rule.
2. **The style picks** — default; deviate only with a recorded row.
3. **`frontend-design/SKILL.md`** — read this file in the skill repository. It governs aesthetic quality, composition, and the refusal to produce generic UI. It owns the concept; the picks own the atoms. Do not invoke `frontend-design` as a registered skill.

They pull in slightly different directions by design. The picker makes components consistent;
reading `frontend-design/SKILL.md` stops the result being a competent, forgettable assembly of catalogue parts.
Both are needed, and this order is how they settle.

---

## MUST / MUST NOT

**Must**
- Personalise the copy with the project's tokens before handing it over — a generic-coloured picker
  defeats the point.
- Namespace the `localStorage` key by run slug.
- Re-bake saved choices into the HTML whenever you touch the run folder.
- Report unchosen components explicitly at the gate.
- Cite `[inferred]` as inferred when explaining a variant to the user.

**Must not**
- Do not write `13-design-brief.md` §6 before the choices are in.
- Do not guess or default a component the user left unchosen without saying so.
- Do not deviate from a pick at stage 15 without a row in the deviations table.
- Do not present the book's metrics as final for Arabic — they are Latin-first starting points.
- Do not ship the book's page images anywhere. The library is our re-implementation of the patterns,
  cited by page. The pages themselves stay in the book.
