# Wireframe Guide — Stage 14

Low-fidelity structural wireframes for **every** screen in `10-screen-list.md`, plus every state
from `11-states-and-edge-cases.md` that changes the layout. No colors, no fonts, no polish —
layout, hierarchy, and behaviour only. This is the stage where structure gets fixed cheaply.

## Read §0 of the design brief first

`13-design-brief.md` §0 names the platform, the design frame, the breakpoints, and the navigation
pattern, confirmed at the stage-13 gate. Everything here follows it. Draw a bottom tab bar on an
admin profile and the whole document is wrong.

## Why the frames use English labels

Arabic text inside a monospace ASCII frame does not work: Arabic glyphs are not monospace-width,
and the Unicode bidi algorithm reorders the neutral box-drawing characters around an RTL run, so
the frame edges scramble and nothing lines up. Anyone who tries it gets a broken box.

So:
- **Inside the frame**: structural English labels — `[Back ›]`, `{Search input}`, `(( avatar ))`.
  Alignment stays perfect and the layout is readable at a glance.
- **Beside the frame**: an Arabic copy table giving the exact Arabic string for every visible
  label. That table is what stage 15 consumes.
- **RTL is expressed by position, not by script** — elements sit where they will actually sit.

The Arabic-language UI is delivered for real at stage 15 in HTML. Nothing is lost here.

## RTL layout conventions in the frames

Draw the screen as the Arabic user sees it. These hold for every platform:

- Back arrow / navigation up: **inline-start**, which in RTL is the **right** edge. Rendered as
  `[‹ Back]` — the chevron points **left**.
- Screen title: right-aligned or centered, per the design brief.
- Header actions (search, filter, notifications): **top-left**.
- List rows: leading element (icon, avatar, thumbnail) on the **right**; trailing element
  (chevron, price, toggle) on the **left**.
- Disclosure chevrons in rows point **left** `‹`.
- Primary action in a form: full-width, or bottom-**right** when actions sit side by side.
  Cancel/secondary sits to its left.
- Progress steppers: step 1 on the right, filling leftwards.
- Text alignment: `start` = right.

### Conventions that differ by platform profile

| | Mobile app | Responsive web / Both | Admin back-office |
|---|---|---|---|
| **Primary nav** | Bottom tab bar; item order right → left, tab 1 is the **rightmost** | Top bar; sidebar anchored **right** below it, drawer under 768 | Persistent sidebar anchored **right**, full height |
| **Secondary nav** | Segmented control or top tabs | Breadcrumbs, reading right → left; dropdown menus opening from the right edge | Breadcrumbs + grouped sidebar sections |
| **Overlays** | Bottom sheet rising from the bottom edge | Centered modal | Modal, or side drawer entering from the **right** |
| **Hover affordances** | None — do not draw them | Mark with `(hover)` in the annotation so stage 15 implements them | Mark with `(hover)`; row hover is expected |
| **Back** | System/app-bar back at top-right | Browser back — draw a breadcrumb, not a back button, unless it is a wizard | Breadcrumb |
| **Density** | Comfortable, 44px minimum rows | Comfortable | Dense — tables, not cards |
| **Bulk actions** | Not drawn | Only if specified | Selection bar with count and action set |

## Frame notation

| Notation | Meaning |
|----------|---------|
| `┌─┐ │ └─┘` | Screen or container boundary |
| `[ Label ]` | Button |
| `[ Label ]*` | Primary button |
| `{ placeholder }` | Text input |
| `{ value ▾ }` | Select / picker |
| `( ) ( • )` | Radio unselected / selected |
| `[ ] [x]` | Checkbox |
| `(( ))` | Avatar / circular image |
| `▨▨▨` | Image or media placeholder |
| `≡` | Menu / list icon |
| `‹` `›` | Chevron (points left in RTL rows) |
| `▬▬▬▬` | Skeleton loading bar |
| `· · ·` | Overflow / more |
| `⌕` | Search |
| `⚠` | Error or warning indicator |
| `S-07` | The screen id, in the frame's title line |

### Frame width by platform profile

Take it from `13-design-brief.md` §0 — do not default to phone.

| Profile | Frame width | Represents |
|---------|------------:|------------|
| Mobile app | 44 characters | 390–360px phone |
| Both — mobile-first | 44 characters | 390px phone, with a desktop adaptation note per screen |
| Responsive web | 100 characters | 1440px desktop |
| Admin back-office | 100 characters | 1440px desktop |
| Tablet, when specified | 76 characters | 768px |

Keep the width consistent across the whole document so it scans. A 100-character frame needs a wide
terminal or editor — that is expected and correct for a desktop product; do not shrink it to fit.

## Per-screen block format

Each screen gets: a heading with its id, the frame, an annotation list, and an Arabic copy table.

````markdown
### S-05 — Search Results · نتائج البحث

**Module**: Browse · **Entry**: S-04, S-03 · **Exits**: S-06 detail, S-04 filters
**Covers**: F-02 steps 3–5 · **States**: default, loading, empty, error (below)

```
┌──────────────────────────────────────────┐
│  ⌕            نتائج البحث          [‹]   │  A
├──────────────────────────────────────────┤
│  { search query                      ⌕ } │  B
│  [ Filter ▾ ] [ Sort ▾ ]      24 results │  C
├──────────────────────────────────────────┤
│ ┌──────────────────────────────────────┐ │
│ │ ‹        Item title             ▨▨▨  │ │  D
│ │          subtitle · meta             │ │
│ │          120 SAR                     │ │
│ └──────────────────────────────────────┘ │
│ ┌──────────────────────────────────────┐ │
│ │ ‹        Item title             ▨▨▨  │ │
│ │          subtitle · meta             │ │
│ └──────────────────────────────────────┘ │
│                  · · ·                   │  E
├──────────────────────────────────────────┤
│   [Profile]  [Orders]  [Search]  [Home]  │  F
└──────────────────────────────────────────┘
```

**Annotations**
- **A** App bar. Back affordance top-right, chevron points left `→ S-04`. Title right of center per
  brief §6. Search icon top-left `→ S-04`.
- **B** Persistent search field, retains the submitted query. Clearing it `→ S-04`.
- **C** Filter and sort chips; active filters show a count badge. Result count is live.
  Filter chip `→ S-09`.
- **D** Result row: thumbnail leads on the right, chevron trails on the left. Whole row is tappable
  (min height 72px) `→ S-06`. Price uses the currency convention in brief §7.
- **E** Infinite scroll; loading tail shows three skeleton rows (E-08).
- **F** Bottom tab bar, rightmost tab is Home `→ S-07`.

**Navigation actions** *(the `→ S-xx` markers above)*

| Element | Position on frame | Goes to | Arabic label |
|---------|-------------------|---------|--------------|
| A back | x 82% · y 2% · w 14% · h 6% | S-04 | رجوع |
| D row | x 4% · y 22% · w 92% · h 11% | S-06 | فتح التفاصيل |
| F Home tab | x 74% · y 93% · w 22% · h 6% | S-07 | الرئيسية |

Positions are **percentages of the frame**, so they survive a frame-size change. This table is what
stage 15c turns into clickable hotspots on `flow-board.html` — author it here, where the layout is
being decided, rather than reverse-engineering it from the HTML later.

**Arabic copy**
| Element | Arabic |
|---------|--------|
| Title | نتائج البحث |
| Search placeholder | ابحث عن... |
| Filter chip | تصفية |
| Sort chip | ترتيب |
| Result count | 24 نتيجة *(Latin digits always)* |
| Tab: Home | الرئيسية |
| Tab: Search | البحث |
| Tab: Orders | طلباتي |
| Tab: Profile | حسابي |

**Behaviour notes**
- Tap row → S-06. Long press → quick actions sheet.
- Pull to refresh re-runs the query.
- Back returns to S-04 with the query preserved.

**Desktop adaptation** *(required when the platform is "Both — mobile-first"; omit otherwise)*
- **F** bottom tab bar → persistent sidebar anchored right, 240px, at ≥ 768.
- **D** single-column rows → 2-column card grid at 768, 3-column at 1440.
- **C** filter and sort chips → a persistent filter rail on the inline-start edge at ≥ 1024.
- **B** search field moves into the top bar; the in-page field is removed.
- Row hover state appears at ≥ 768 (pointer only) — background tint, no layout shift.
````

## Desktop adaptation notes

Required for **every screen** when the platform profile is "Both — mobile-first". One short list per
screen, placed beneath the behaviour notes, naming only what changes:

- **What moves** — which element relocates, and to where.
- **What reflows** — column counts at each breakpoint.
- **What changes type** — sheet → modal, tab bar → sidebar, full-width CTA → inline button.
- **What appears or disappears** — hover states appear on pointer; a mobile-only affordance such as
  pull-to-refresh disappears and needs a visible refresh control instead.

Global rules that apply to every screen live once in `13-design-brief.md` §0 under *Desktop
adaptation rules*. Reference them (`per brief §0`) rather than restating them per screen; list here
only what is specific to this screen.

This list is the contract stage 15 implements. A screen with no adaptation note on a "Both" profile
means the responsive HTML will be guessed — so the coverage table checks for it.

## State variants

For each screen, draw a separate small frame for every state in `11-states-and-edge-cases.md`
that changes the layout. Skip states that only change a color or a single string — note those in
the annotations instead.

```
S-05 · Empty — no results          S-05 · Error
┌──────────────────────────┐       ┌──────────────────────────┐
│   نتائج البحث      [‹]   │       │   نتائج البحث      [‹]   │
├──────────────────────────┤       ├──────────────────────────┤
│ { query "xyz"        ⌕ } │       │ { query              ⌕ } │
│                          │       │                          │
│          ▨▨▨▨            │       │           ⚠              │
│      No results for      │       │   Couldn't load results   │
│       "xyz" found        │       │                          │
│   Try different words    │       │      [ Retry ]*          │
│                          │       │                          │
│   [ Clear filters ]      │       │                          │
└──────────────────────────┘       └──────────────────────────┘
```

Each variant carries its own Arabic copy rows.

## Document structure — `14-wireframes.md`

```markdown
# Wireframes — <Product Name>

Low-fidelity. Structure and behaviour only; visual design is defined in `13-design-brief.md`
and implemented in `15-ui-designs/`.

**Platform**: <from brief §0> · **Frame**: <44 or 100 chars, representing 390 or 1440px> ·
**Navigation**: <bottom tab bar | right-anchored sidebar>

## Coverage
| Screen | Frame | States drawn | Desktop adaptation |
|--------|:-----:|--------------|:------------------:|
| S-01 Splash | ✅ | default | n/a — mobile only |
| S-05 Search results | ✅ | default, loading, empty, error | ✅ |
<one row per screen in 10-screen-list.md — no gaps>

The **Desktop adaptation** column is required when the platform is "Both — mobile-first" and shows
`n/a` on every other profile. An empty cell on a "Both" profile is a gap, not a blank.

## Global patterns
Drawn once, referenced everywhere: header, primary navigation (bottom tab bar on mobile, right-anchored
sidebar on web and admin), list row, table row on admin profiles, form field group, empty state,
error state, loading skeleton, confirmation overlay (sheet on mobile, modal on web), toast.

## Screens
<grouped by module, in flow order, using the per-screen block format>

## Open layout questions
<anything the wireframes could not resolve without a decision>
```

## Quality bar

- Every screen in `10-screen-list.md` has a frame. The coverage table proves it — no gaps, no
  "similar to S-05" placeholders.
- **Every frame is drawn at the width the platform profile specifies**, with that profile's
  navigation pattern. No bottom tab bar on a web or admin profile; no hover affordance on mobile.
- On a "Both — mobile-first" profile, every screen carries a desktop adaptation note.
- Every frame's RTL positions are correct: back on the right, chevrons pointing left, tab order
  right-to-left, sidebar anchored right.
- Every visible string has an Arabic value in the copy table. Stage 15 must not have to invent copy.
- Annotations explain behaviour, not appearance. "Opens the filter sheet" — not "rounded corners".
- **Every element that navigates carries a `→ S-xx` marker and a row in the navigation-actions
  table**, with its position in percentages. Stage 15c builds the flow board's hotspots from these;
  a missing row means a dead hotspot the client cannot click.
- Global patterns are drawn once and referenced, not redrawn per screen.

## The gate

Summarize: screen count, state-variant count, and the layout decisions you made that the brief and
requirements did not dictate. Offer options like *Approve and build the HTML* / *Rework specific
screens* / *Change a global pattern* / *Add missing screens*. Only after approval does stage 15 begin.
