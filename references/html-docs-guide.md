# Interactive HTML Documentation Guide — Stage 17

Render the fifteen approved markdown documents as an interactive HTML documentation site in
`docs-html/`, following the patterns in
[anthropics/html-effectiveness](https://github.com/anthropics/html-effectiveness).

The point is not decoration. Markdown cannot filter a 60-row screen list or a 40-story backlog,
cannot render a Mermaid diagram in most viewers, and leaves `S-05` as dead text instead of a jump to
the screen. Stage 17 fixes exactly that. Every interactive affordance must earn its place by making
the content easier to navigate, verify, or hand to a development team.

This site is the front door of the handoff. A backend engineer should be able to open it and reach
the API surface, the data model, and the permission matrix in three clicks; a QA lead should be able
to filter test coverage by screen; a client should be able to click through the Arabic UI.

**docs-html is English and LTR** — it mirrors the source documents. Arabic appears only where the
source has it (glossary, Arabic UI titles, wireframe copy tables), inside `dir="rtl"` spans with
`<bdi>` isolation around embedded numerals. The Arabic RTL product UI lives in `15-ui-designs/`
and is linked, not duplicated.

---

## 1. Design tokens — the house palette

Copy this block verbatim into `docs.css`. It is the shared `:root` used across all 21 files in the
reference repo. Do not adjust the values.

```css
:root {
  /* surface + ink */
  --ivory:    #FAF9F5;
  --white:    #FFFFFF;
  --slate:    #141413;

  /* accents */
  --clay:     #D97757;
  --clay-d:   #B85C3E;
  --oat:      #E3DACC;
  --olive:    #788C5D;
  --rust:     #B04A3F;

  /* neutrals */
  --gray-150: #F0EEE6;
  --gray-300: #D1CFC5;
  --gray-500: #87867F;
  --gray-700: #3D3D3A;

  /* semantic */
  --warning:  #C78E3F;
  --danger:   #B04A4A;
  --info:     #5C7CA3;

  /* type */
  --serif: ui-serif, Georgia, "Times New Roman", serif;
  --sans:  system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  --mono:  ui-monospace, "SF Mono", Menlo, Consolas, monospace;

  /* shape */
  --radius-panel: 12px;
  --radius-row:   8px;
  --border: 1.5px solid var(--gray-300);
}
```

Serif for headings, sans for body, mono for metadata and code. **No web fonts** in the docs chrome —
system stacks only. No dark mode. No frameworks, no CDN, no build step.

## 2. The two-palette rule

This is the rule most likely to be broken. Read it twice.

- **Documentation chrome uses the house palette above.** Page background, headings, body text,
  tables, chips, nav, borders, links, severity dots. Every page, every section.
- **Anywhere the docs display the product's own design system, the product's palette is used.**
  Color swatches, type specimens, component previews, wireframe previews, screen thumbnails —
  these must show what the client is actually getting, not ivory and clay.

Implement it with a scoped token block. Emit the product tokens from design brief §9 into a
`.product-surface` scope, namespaced `--p-*`:

```css
.product-surface {
  --p-primary:    #0F5F4E;   /* from 13-design-brief.md §9 */
  --p-on-primary: #FFFFFF;
  --p-surface:    #FFFFFF;
  --p-text:       #14201C;
  --p-radius-md:  12px;
  /* …every token in the brief */

  background: var(--p-surface);
  border: var(--border);
  border-radius: var(--radius-panel);
  padding: 24px;
}
```

Anything rendered inside `.product-surface` uses `--p-*` exclusively. Anything outside it uses the
house tokens exclusively. Never `--clay` for a product button; never `--p-primary` for docs chrome.

Mark product regions visually so no one mistakes a preview for the documentation itself — a mono
`.eyebrow` label above each one reading `product preview` is enough.

## 3. Folder contract

```
docs-html/
  index.html                       dashboard, gallery, coverage matrix, readiness panel
  docs.css                         house tokens + all shared components
  docs.js                          shared interaction layer
  01-prd.html
  02-business-rules.html
  03-use-cases.html
  04-permission-matrix.html
  05-srs.html
  06-data-model.html
  07-api-surface.html
  08-user-stories.html
  09-user-flows.html
  10-screen-list.html
  11-states-and-edge-cases.html
  12-test-scenarios.html
  13-design-brief.html
  14-wireframes.html
  16-traceability-matrix.html
  README.md                        what this is, how to open, verification results
```

Fifteen content pages plus the index — sixteen HTML files in all. There is no `15-ui-designs.html` — stage 15's output is
already a browsable gallery at `../15-ui-designs/index.html`, and stage 17 **links** to it rather
than copying or re-rendering it. Keep the numbering aligned with the markdown files so a reader can
map between the two sets without a lookup table.

Everything opens over `file://` with no server and no build. `docs.css` and `docs.js` are the only
shared assets; a page may add a small page-scoped `<style>` block for anything genuinely local.

## 4. Content-in-HTML rule

The reference repo's `18-editor-triage-board.html` builds its DOM from a JS array, which means it
is blank with JavaScript disabled. **Do not do that here.**

- All content lives in the HTML markup.
- JavaScript only filters, reveals, selects, links, and computes.
- Every page must read completely with JS off — that keeps the docs printable, greppable, and
  survivable when a script throws.

Where a page needs structured data for interaction (screen metadata for the detail panel, node
detail for the flow sidebar), put it in `data-*` attributes on the elements that already carry the
visible content, not in a separate array.

## 5. Layout primitives

```css
.page   { max-width: 1120px; margin: 0 auto; }   /* index, wide tables */
.sheet  { max-width: 980px;  margin: 0 auto; }   /* standard document page */
.narrow { max-width: 860px;  margin: 0 auto; }   /* long-form reading */
body    { background: var(--ivory); color: var(--slate);
          font-family: var(--sans); font-size: 15px; line-height: 1.6;
          padding: 56px 24px 120px; }
section { margin-bottom: 56px; }
```

Two-column detail layouts (flow diagram + sidebar, screen list + detail panel):

```css
.layout { display: grid; grid-template-columns: minmax(0,1fr) 300px;
          gap: 32px; align-items: start; }
@media (max-width: 920px) { .layout { grid-template-columns: 1fr; } }
```

Breakpoints: `920px` (collapse two-column layouts and 4-col grids to 2) and `720px` (single column,
reduce body padding to `40px 16px 80px`).

## 6. Shared component classes for `docs.css`

Build these once; every page uses them.

### Structure and headings
| Class | Renders |
|-------|---------|
| `.eyebrow` | mono, 12px, uppercase, `letter-spacing:.08em`, `--gray-500`; the small label above a title |
| `.page-head` | document masthead: eyebrow, `h1` (serif, 38px, weight 500, `-0.01em`), subtitle |
| `.sec-head` | section header row: `.idx` (mono ordinal), `h2` (serif 26px), `.count` pill |
| `.count` | pill counter, `background:var(--gray-150)`, `border-radius:999px`, `padding:1px 8px` |
| `.prompt-box` | gray rounded panel showing the source brief; mono label + quoted content |
| `.topbar` | sticky cross-document nav: run name on the left, links to all 16 pages on the right |
| `.toc` | sticky per-page contents with scroll-spy, `position:sticky; top:24px` |

### Data display
| Class | Renders |
|-------|---------|
| `.summary-band` | `grid-template-columns:repeat(4,1fr); gap:14px` of `.stat-card` |
| `.stat-card` | white panel; `.stat-num` (serif 44px), `.stat-label` (uppercase 12px), `.stat-delta` (mono 11px). `.stat-card.warn` adds `border-left:4px solid var(--clay)` |
| `table.data` | bordered table, `th` sans 11px weight 600 uppercase, alternating row backgrounds, `tbody tr:hover{background:var(--ivory)}` |
| `.matrix` | dense grid table for the coverage and state matrices; cells `✅ / ❌ / ⚠ / —` |
| `.risk-dot` | 9px circle; `.low`→`--olive`, `.med`→`--clay`, `.high`→`--rust` |
| `.badge` | inline pill; variants `.badge-neutral .badge-accent .badge-success .badge-warning .badge-danger` |
| `.tag` | mono 11px chip on `--gray-150`; used for ids, modules, roles, provenance |
| `.q` | white card with `border-left:3px solid var(--clay)`; title, body, owner line — assumptions and open questions |
| `.callout` | bordered note block; `.callout.warn` clay, `.callout.info` info blue |
| `.legend` | flex row of `<span><i class="chip"></i> label</span>`; `.chip` is a 22×14px bordered `<i>`, `.chip.gate` rotated 45°, `.chip.ok` olive, `.chip.bad` rust |
| `.milestone` | timeline row, `grid-template-columns:120px 28px 1fr` with `.dot` / `.dot.done` / `.line` |
| `.code` | dark block, `background:var(--slate)`, mono 12.5px, line-height 1.65, spans `.kw .str .cm .fn` |
| `.frame` | `<pre>` for ASCII wireframes; mono, `direction:ltr`, `white-space:pre`, no wrapping, horizontal scroll on overflow |

### Interaction affordances
| Class | Renders |
|-------|---------|
| `.card` | linked gallery card; `border-radius:14px`, hover `translateY(-3px)` + shadow + border darken |
| `.grid` | `repeat(auto-fill, minmax(316px,1fr)); gap:16px` |
| `.filter-bar` | search input + chip row + live `.result-count` |
| `.chip-btn` | toggleable filter chip; `.on` state fills with `--oat` and darkens the border |
| `.master` / `.detail` | the two halves of a master-detail pane; `.row.selected` gets a clay `border-inline-start` |
| `.tabs` / `.tab` | tab strip; `.tab.on` gets a 2px clay bottom border |
| `.expandable` | collapsible card; `.expandable > .head` is the button, `[aria-expanded]` drives the body |
| `.dim` | 0.35 opacity for filtered-out items that stay in the DOM |
| `.anchor-link` | `#` link revealed on heading hover |

### Arabic content inside the docs
```css
.ar { direction: rtl; text-align: right; unicode-bidi: isolate;
      font-family: "Noto Sans Arabic", "Segoe UI", Tahoma, sans-serif;
      line-height: 1.85; }
td.ar, .ar-cell { direction: rtl; text-align: right; unicode-bidi: isolate; }
```
Wrap embedded numerals and Latin words in `<bdi>`. Never let an Arabic string inherit the page's
LTR alignment.

## 7. `docs.js` — the shared interaction layer

Plain ES5-compatible vanilla JS, no modules, no bundler, loaded with `<script src="docs.js" defer>`.
Each function is a no-op when its markup is absent, so every page can call `init()` unconditionally.

| Function | Behaviour |
|----------|-----------|
| `initTopbar()` | marks the current page's link `.on` from `location.pathname` |
| `initTOC()` | builds the sticky contents from `h2[id]`/`h3[id]`, highlights via `IntersectionObserver` |
| `initAnchors()` | appends a `#` `.anchor-link` to every heading with an `id` |
| `initFilters()` | chip filtering over `[data-tags]`; multiple active chips are OR within a group, AND across groups; updates `.result-count`; adds `.dim` rather than removing nodes |
| `initSearch()` | debounced text filter matching against `[data-search]` (a lowercased string of the row's searchable text) |
| `initMasterDetail()` | click a `.row` → mark `.selected`, render its `data-*` payload into `.detail`, and push `#ID` to the URL with `history.replaceState` |
| `initTabs()` | `.tab` click toggles `.on` and shows the matching `[data-panel]` |
| `initExpand()` | toggles `.expandable`, keeping `aria-expanded` in sync |
| `initFlowNodes()` | click an SVG `.node[data-k]` → set `.active`, populate the flow detail sidebar from that node's `data-*` attributes |
| `initDeepLink()` | on load and on `hashchange`, resolve `#S-05` / `#UC-03` / `#E-07` — select the row, open the tab or card that contains it, and scroll it into view |
| `contrastRatio(fg, bg)` | WCAG 2.1 relative luminance ratio from two hex strings; returns a number |
| `paintContrastBadges()` | for every `[data-fg][data-bg]`, compute the ratio and render `4.8:1 · AA` or `3.1:1 · fail` |
| `initCopyMarkdown()` | rebuilds a markdown view of the page from the DOM and copies it, mirroring the repo's `buildMarkdown()` export |

Guard everything: `if (!el) return;`. A missing section on one page must not break the others.

## 8. Per-document mapping

### `index.html` — dashboard, gallery, readiness
*Patterns: the repo's `index.html` gallery + `11-status-report.html` stat band.*

- `.page-head` masthead: eyebrow with the run id, product name as `h1`, one-line purpose.
- `.summary-band` of `.stat-card`, two rows: business rules · use cases · functional requirements ·
  non-functional requirements / entities · endpoints · epics · stories · story points · flows ·
  screens · edge cases · test cases. **Counts are computed by reading the source documents**, never
  estimated. They must equal the counts table in `16-traceability-matrix.md` §7.
- **Handoff readiness panel** — the readiness table from `16-traceability-matrix.md` §6 rendered as
  pass/warn tiles (complete · traceable · testable · buildable · specified · secure · localized).
  Any warn tile links straight to the gap in `16-traceability-matrix.html`. This is the first thing
  a reader sees after the counts, because it is the honest status of the package.
- `.prompt-box` holding the original Arabic requirement verbatim, in a `.ar` block.
- `.grid` of `.card` links — one per document — each with a small inline-SVG thumbnail hinting at the
  page's content (a rules table, an ERD, a flow graph, a screen grid, a swatch row), a one-line
  description, the **primary owner role**, and the filename in mono. Group the cards under the
  headings *Requirements* (01–04), *Specification* (05–07), *Delivery* (08, 12), *UX* (09–11),
  *Design* (13–15), *Assurance* (16).
- **Reading order by role** — the table from `README.md`, with every id linked.
- A **platform badge** in the masthead — `mobile app · 390×844` or `responsive web · 1440` — taken
  from `13-design-brief.md` §0. It is the second-most important fact about the run after the product
  name, and it stops anyone reviewing the package against the wrong mental model.
- **Two cards linking out to the stage-15 surfaces**, set apart from the document cards since they
  are live product rather than documentation:
  - `../15-ui-designs/index.html` — *the catalogue*: every screen in a device frame, grouped by
    module. Labelled with the platform and frame size.
  - `../15-ui-designs/flow-board.html` — *the client-review board*: the whole product as a journey
    map, screens in flow position with labelled arrows, zoomable and clickable. Mark this one as
    **the file to send a client**, because that is what it is for and nobody will guess.
- Footer with run metadata: folder, date, source language, stage approvals from `00-run-log.md`.

### `01-prd.html`
*Patterns: `16-implementation-plan.html` + `14-research-feature-explainer.html`.*

This page renders `01-prd.md`. It does not add a BRD page. Link `brd.md` only from the PRD's
related-documents table when that file exists. Do not add `brd.html` to the default page set.

- Executive summary and problem statement as prose in `.narrow`.
- `G-xx` objectives as a `table.data` with success measure, baseline, and target; non-goals as a
  `.callout`.
- `P-xx` persona cards in a `.grid` — who / goal / frustrations / success — with the id as a `.tag`.
- Scope in/out as two columns; release phasing as a `.milestone` timeline.
- `A-xx` assumptions and `Q-xx` open questions as `.q` cards, with blocking items marked
  `.badge-danger` and sortable to the top. Do not render an assumption as a confirmed requirement.
- Confirmed product behavior (§12), the product-level permissions summary (§13), and any
  acceptance criteria the source already stated (§14). Do not duplicate the permission matrix,
  the SRS, or the story acceptance criteria on this page.
- Glossary `table.data` with the Arabic column in `.ar-cell`.
- Related-documents card row linking 02/03/04/05/08. Include `brd.md` only when that file exists.

### `02-business-rules.html`
*Pattern: `18-editor-triage-board.html`.*

- `.filter-bar`: search, plus chip groups for category (validation · calculation · authorization ·
  lifecycle · temporal · data integrity), enforcement point (client · server · both), and provenance
  (arabic source · assumption). Live result count.
- Rules as `table.data` rows anchored `#BR-01`, each linking to its `FR-xx`, `UC-xx`, and `TC-xx`.
- Provenance rendered as a `.tag`; `assumption` gets `.badge-warning`, and a client-only enforcement
  point gets `.badge-danger` since it is almost always a defect.
- Calculation rules in `.expandable` cards with the formula in a `.code` block and the worked-example
  table beneath.
- Lifecycle state machines as small inline SVGs using the §9 recipe.

### `03-use-cases.html`
*Pattern: `16-implementation-plan.html`.*

- Actor filter chips and a search box.
- Index `table.data` first, then **`UC-xx` as `.expandable` cards** — collapsed shows id, title,
  actor, priority, and the `G-xx` it serves; expanded shows trigger, preconditions, guarantees, the
  numbered main flow, alternates, the failure-path table, postconditions, and links to `BR-xx`,
  `F-xx`, `S-xx`, `FR-xx`.
- Actor × use-case `.matrix` with ● / ○ cells.
- A use case with no failure path is flagged inline with a `.callout.warn` — it is incomplete.

### `04-permission-matrix.html`
*Pattern: `19-editor-feature-flags.html`.*

- The capability matrix as an interactive `.matrix`: hovering a cell highlights its row and column
  (cross-hair), and a role chip filter collapses the table to a single-role view.
- Every `⚠️` cell is a button that reveals its footnote inline rather than sending the reader to the
  bottom of the page.
- Data-scope, field-level, and state-transition tables below, each filterable by role.
- **Unauthenticated surface** section rendered as a `.callout.warn` — it is the attack surface, so it
  gets visual weight.
- Every capability links to the `API-xx` that exposes it, and every cell links to its `BR-xx`.

### `05-srs.html`
*Patterns: `16-implementation-plan.html` + `14-research-feature-explainer.html`.*

- Module and priority filter chips, plus search.
- System context diagram as inline SVG (§9 recipe).
- **`FR-xx` cards** with the EARS clause typeset distinctly — `While`/`When`/`Where`/`shall` in
  `--clay` mono so the pattern is visible at a glance, the rest in body type. Metadata row of `.tag`s:
  realizes `UC-xx`, enforces `BR-xx`, priority, verification method.
- **`NFR-xx` as `.stat-card` tiles** showing the numeric target large — the number is the point. A
  target rendered without a number is a bug in the source document; flag it with `.stat-card.warn`.
- External interfaces, constraints, and the verification table as `table.data`.

### `06-data-model.html`
*Pattern: `13-flowchart-diagram.html` — reuse the §9 recipe.*

- **Inline-SVG ERD** as the hero: entities as `rect rx="8"` nodes carrying `data-k="EN-03"`,
  relationships as `.edge` paths with cardinality labels at each end (crow's-foot rendered as a
  small three-line marker, or `1` / `n` text labels — pick one and stay consistent).
- Clicking an entity fills the 300px detail sidebar with its full attribute table.
- Entity dictionary below the diagram, each anchored `#EN-03`, attributes as `table.data` with PII
  fields marked `.badge-warning` and rule links in the last column.
- Enumerations, conventions, and volume tables as plain `table.data`.

### `07-api-surface.html`
*Patterns: `03-code-review-pr.html` + `04-code-understanding.html`.*

- Filter chips for resource, HTTP method, and auth level; search over path and description.
- Endpoint rows with **method badges** — GET `--info`, POST `--olive`, PATCH/PUT `--warning`,
  DELETE `--rust` — the path in mono, and the required permission as a `.tag` linking to
  `04-permission-matrix.html`.
- Each row `.expandable` to reveal request and response shapes in `.code` blocks with JSON syntax
  spans, plus the error `table.data` with each code linked to its `BR-xx`.
- Use-case coverage table with uncovered rows highlighted `--rust`.
- The "this is a sketch, not OpenAPI" caveat as a `.callout` at the top — it must not be missed.

### `08-user-stories.html` — the backlog board
*Pattern: `18-editor-triage-board.html`. This is the richest interactive page in the set.*

- Summary band: total stories, total points, and points by MoSCoW priority.
- **Board view**: one column per `EP-xx` epic, story cards within, each showing id, title, points,
  and priority. Column headers carry a running point total that updates as filters apply.
- Filter chips for MoSCoW priority, epic, and role; search over story text. Filtered-out cards get
  `.dim` rather than being removed, so the shape of the backlog stays visible.
- Each story card is `.expandable` — opening it reveals the As-a/I-want/So-that statement, the full
  Given/When/Then acceptance criteria, and `.tag` links to `FR-xx`, `BR-xx`, `S-xx`, `API-xx`.
- **Dependency links**: `depends on` / `blocks` render as clickable ids that scroll to the target
  card and flash it.
- Release slicing table below the board, and the definition of done as a `.callout` checklist.
- A story of 13 points or more carries a `.badge-warning` reading `split me`.

### `09-user-flows.html`
*Pattern: `13-flowchart-diagram.html`.*

- `.tabs` switch between flows `F-01`, `F-02`, …
- Each flow renders as **hand-authored inline SVG** (recipe in §9) inside `.layout`, with a 300px
  detail sidebar on the right.
- Clicking a node sets `.active` (clay stroke, 2px) and fills the sidebar from that node's
  `data-title` / `data-meta` / `data-body` / `data-screen` attributes: the step narrative, the
  `BR-xx` enforced there, and a link to the `S-xx` screen in `10-screen-list.html`.
- `.legend` chips: process step · decision · terminal success · failure path.
- Below the diagram: the decision-point `table.data` and the failure/exit `table.data` from the
  source, with every `BR-xx`, `S-xx`, and `E-xx` linked.

### `10-screen-list.html`
*Patterns: `18-editor-triage-board.html` + `06-component-variants.html`.*

- `.filter-bar`: search input, module chips, role chips, live result count, clear-all.
- `.layout` master-detail — `.master` is the full screen list grouped by module, each `.row`
  carrying `id="S-05"`, `data-tags="module-browse role-customer"`, `data-search="…"`, and the detail
  payload in `data-*`.
- `.detail` panel shows purpose, Arabic UI title (`.ar`), entry points, exits, key components, data
  shown, actions, roles, and the `FR-xx` it surfaces — plus links to the wireframe anchor
  (`14-wireframes.html#S-05`), the states section (`11-states-and-edge-cases.html#S-05`), the tests
  (`12-test-scenarios.html#S-05`), and the live screen
  (`../15-ui-designs/08-search-results.html`).
- `[implied]` screens carry a `.badge-warning` so the client can see what was added beyond the source.
- Deep-linkable: `10-screen-list.html#S-05` opens with that screen selected and scrolled to.

### `11-states-and-edge-cases.html`
*Patterns: `12-incident-report.html` + `11-status-report.html`.*

- **State matrix**: screens down the rows, state types across the columns (default, loading, empty,
  error, offline, partial, unauthorized, success). Cells show defined / not applicable / missing.
  Missing cells are the point — they surface gaps at a glance and are tinted `--rust`.
- Chip filters per state type dim non-matching rows.
- Per-screen state detail sections, anchored `#S-05`, each linking back to the screen and forward to
  its `TC-xx`.
- Account/session states as a `.milestone` timeline.
- Cross-cutting edge cases as a `table.data` with `.risk-dot` severity, `E-xx` anchors, and every
  `BR-xx` / `S-xx` / `TC-xx` mention linked.
- Empty-state and error-message inventory tables.

### `12-test-scenarios.html`
*Patterns: `11-status-report.html` + `12-incident-report.html`.*

- Summary band of counts by test type.
- **Coverage matrix** — screens down, test types across — with empty cells tinted `--rust` and a
  toggle to show only rows with gaps. This is the page's headline: what is *not* tested.
- Filter chips for type and priority; search over title and preconditions.
- `TC-xx` cases as `.expandable` rows: steps as an ordered list, expected result as a `.callout`,
  and `.tag` links to `US-xx`, `AC-xx`, `FR-xx`, `BR-xx`, `S-xx`.
- The Arabic/RTL and accessibility test sets get their own clearly headed sections — they are the
  first thing that gets dropped under pressure, so they are visually prominent.
- "Untested by design" rendered as a `.callout.warn`, never hidden.

### `13-design-brief.html`
*Pattern: `05-design-system.html`.*

This is the page where the product palette takes over. Everything below the section headers sits
inside `.product-surface`.

- **Platform profile card, first thing on the page** — §0 of the brief rendered as a `.summary-band`
  of `.stat-card` tiles: platform, design frame, breakpoints, navigation pattern, input model. A
  frontend engineer opening this page must see the frame size before anything else, because it is
  what they build against. Below the tiles, the target devices and chrome allowances as a compact
  `table.data`, and — on a "Both — mobile-first" profile — the **desktop adaptation rules** table.
  This card uses **house chrome**, not product tokens: it is documentation about the product, not a
  sample of it.
- Brand identity, audience, and visual style as prose sections in house chrome.
- **`.swatch-grid`** of the product's colors: 64px chips, hex, token name, usage rule, and a
  **computed contrast badge** — `paintContrastBadges()` calculates the ratio from the actual hex
  values rather than trusting the table in the markdown. Any pair failing AA is flagged.
- **`.type-scale`** specimens set in the real Arabic families, loaded from Google Fonts **on this
  page only**, rendered with Arabic sample text at each size, with `name / size / line-height /
  weight` metadata in mono.
- `.spacing-ruler` bars, radius cards, elevation cards — in product tokens.
- **Live component specimens** rendered `dir="rtl"` in product colors: buttons in every variant and
  state, inputs with label/helper/error, cards, list rows, nav, badges, toasts. Each labelled with
  its spec from the brief.
- RTL and localization rules as a `table.data`.
- Do / Don't table with `.badge-success` / `.badge-danger` markers.

### `14-wireframes.html`
*Patterns: `04-code-understanding.html` + `01-exploration-code-approaches.html`.*

- Screen filter and module chips at the top, plus the platform and frame width stated in the
  `.page-head` subtitle — a 100-character frame needs a wider `<pre>` than a 44-character one, and
  the reader should know which they are looking at.
- Per screen: `.layout` with the ASCII frame in `<pre class="frame">` on the left — LTR, mono,
  alignment preserved, horizontally scrollable — and the numbered annotation list on the right.
- The Arabic copy `table.data` beneath, with the Arabic column in `.ar-cell`.
- On a "Both — mobile-first" profile, the **Desktop adaptation** list renders as a `.callout` beneath
  the annotations, visually distinct so it is not mistaken for the mobile spec.
- State variants as `.tabs` within each screen block.
- Each screen block anchored `#S-05`, with a back-link to `10-screen-list.html#S-05` and a forward
  link to the live HTML screen in `../15-ui-designs/`.
- Global patterns section first, drawn once and referenced.

### `16-traceability-matrix.html`
*Pattern: `18-editor-triage-board.html`.*

- The **gap report first**, above the matrices — `GAP-xx` rows as `.q` cards with a `--rust` left
  border, each linking to both ends of the broken chain. If there are no gaps, render an explicit
  "no gaps found" `.callout`, never an empty section.
- Handoff readiness table as pass/warn tiles, matching the panel on `index.html` exactly.
- The four chain matrices as filterable `table.data`, each cell a link. **Orphan cells are tinted
  `--rust`** and a chip toggles "show only rows with gaps".
- Counts table last.

## 9. Inline SVG flowchart recipe

Convert each Mermaid block in `09-user-flows.md` by hand — and reuse this same recipe for the ERD in
`06-data-model.html`, the lifecycle state machines in `02-business-rules.html`, and the system
context diagram in `05-srs.html`. No Mermaid, no chart library.

**Canvas**: `<svg class="flow" viewBox="0 0 620 H">` where `H` grows with the node count.
Vertical rhythm of ~76px between node centers; center column at `x=310`; branch columns at
`x=150` and `x=470`.

**Nodes** — a `<g class="node" data-k="…">` wrapping the shape and its labels:
| Kind | Markup |
|------|--------|
| Process step | `<rect rx="8" width="164" height="48">` |
| Terminal | `<rect rx="22" width="164" height="44">` |
| Decision | `<path d="M310,262 L352,294 L310,326 L268,294 Z">` |
| Success terminal | `.node.ok` — olive stroke, `rgba(120,140,93,.12)` fill |
| Failure terminal | `.node.bad` — rust stroke, `rgba(176,74,63,.12)` fill |

Node text is `<text text-anchor="middle">` for the label plus `<text class="sub">` for secondary
detail (the screen id, the rule, the duration).

**Edges**: `<path class="edge" d="M310,56 L310,92" marker-end="url(#arrow)"/>`. Use cubic curves for
branch routing: `M268,294 C190,294 150,294 150,212`. Edge labels are `<text class="edge-label">`
placed at the midpoint with a small ivory `<rect>` behind them so the line does not strike through.

**Markers** — three, defined once in `<defs>`:
```html
<marker id="arrow"       viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6"
        orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#87867F"/></marker>
<marker id="arrow-rust"  … fill="#B04A3F"/>
<marker id="arrow-olive" … fill="#788C5D"/>
```
Failure edges use `arrow-rust` and a rust stroke; success edges use `arrow-olive`.

**Interaction**: `.node { cursor:pointer; transition: transform 120ms ease }`,
`.node:hover { transform: translateY(-1px) }`, `.node.active` gets `stroke: var(--clay);
stroke-width: 2`. `initFlowNodes()` wires the click to the sidebar. Load with the first node active.

**Accessibility** — the one place to improve on the reference repo: give each `<svg>` a
`role="img"` and an `<title>`/`<desc>`, make each node focusable (`tabindex="0"`) and activatable by
Enter/Space, and keep the full step narrative in the visible tables below so the diagram is never
the only source of the information.

## 10. Accessibility floor for docs-html

The reference files are light on this. Meet at least:

- Semantic HTML — real `<button>` for anything clickable, `<nav>`, `<main>`, `<table>` with `<th
  scope>`, correct heading hierarchy.
- Visible `:focus-visible` ring on every interactive element.
- `aria-expanded` on expandables, `aria-selected` on tabs, `aria-live="polite"` on the result count.
- Filter and search controls have real `<label>`s.
- Docs chrome text meets WCAG AA against `--ivory`.
- Never signal state with color alone — pair every `.risk-dot` with its text label.
- `@media (prefers-reduced-motion: reduce)` disabling transforms and transitions.

## 11. Verification protocol — stage 17c

Run all four passes and report the results as a table at the gate. Do not claim the stage is done
without it. State failures plainly and fix them before gating.

### Accuracy — every fact traces to a source document
1. Every id in the registry (`G BR UC FR NFR EN API EP US AC F S E TC A Q GAP`) that appears in the
   HTML exists in the markdown with the same title. Cross-check **both** directions.
2. Every `.stat-num` recomputed from the source matches what is rendered, and matches the counts
   table in `16-traceability-matrix.md` §7.
3. The readiness panel on `index.html` matches `16-traceability-matrix.md` §6 tile for tile, and the
   gap list on `16-traceability-matrix.html` matches §5 row for row.
4. Every Arabic string is byte-identical to the source — no re-translation, no paraphrase, no
   "improved" copy.
5. Nothing in the HTML is absent from the markdown. Spot-check three sections verbatim.
6. Contrast badges are computed from the real hex values, not copied from the brief's table.

### Completeness — nothing dropped
7. Fifteen content pages exist plus `index.html`. Name any missing.
8. Every `##` and `###` heading in each source document has a home in its HTML page. List omissions.
9. Screen count in `10-screen-list.html` equals the count in `10-screen-list.md`; story and point
   totals in `08-user-stories.html` equal `08-user-stories.md`; test count in
   `12-test-scenarios.html` equals `12-test-scenarios.md`.
10. Every flow in `09-user-flows.md` has a rendered SVG — no "see the markdown" placeholders. Same
    for the ERD in `06-data-model.html` and the system context diagram in `05-srs.html`.
11. Every state variant in `14-wireframes.md` appears as a tab.
12. Every `⚠️` cell in the permission matrix has its footnote reachable inline.

### Effectiveness — the HTML beats the markdown
13. Any screen, story, endpoint, or test case is reachable in ≤ 3 interactions from `index.html`.
14. Every cross-reference is a working link, including cross-page deep links like
    `11-states-and-edge-cases.html` → `10-screen-list.html#S-05` and
    `08-user-stories.html` → `05-srs.html#FR-18`.
15. Filters and search return correct results on every page that has them; clearing restores the
    full set; the count is right; the backlog board's per-epic point totals update with the filter.
16. Every page reads completely with JavaScript disabled.
17. Renders correctly at 1440px, 1024px, and 768px.
18. No horizontal scroll except inside `<pre class="frame">`, where it is intended.

### Mechanical checks

Run these from the run folder in Windows PowerShell. They do not require `rg`, Bash, or GNU `grep`. Use another search command only after you have confirmed that command exists in this session.

```powershell
# Markdown links that should be .html
Select-String -Path 'docs-html\*.html' -Pattern '\]\(.*\.md\)' -CaseSensitive
# Unconverted diagrams
Select-String -Path 'docs-html\*.html' -Pattern 'mermaid|flowchart TD|erDiagram' -CaseSensitive
# Placeholder leftovers
Get-ChildItem -Path 'docs-html' -Recurse -File | Select-String -Pattern 'lorem|TODO|FIXME|xxx'
# Confirm src and href attributes are present to inspect
Select-String -Path 'docs-html\*.html' -Pattern 'src=|href=' -CaseSensitive
# The UI gallery is linked from the docs index
Select-String -Path 'docs-html\index.html' -Pattern '15-ui-designs' -CaseSensitive
```

Report as:

| Pass | Checks | Result |
|------|--------|--------|
| Accuracy | 6 | ✅ 6/6 |
| Completeness | 6 | ⚠️ 5/6 — F-03 diagram missing, added |
| Effectiveness | 6 | ✅ 6/6 |
| Mechanical | 5 | ✅ 5/5 |

## 12. `docs-html/README.md`

Short. What this is, that it needs no server, `index.html` is the entry point, a one-line
description of each of the fifteen pages, the verification table from §11, and the date it was
generated from which run.

## 13. The gate

Summarize: pages produced, the counts rendered, the verification table, the handoff readiness
result, anything the source documents left ambiguous that you had to resolve, and any gap the
coverage matrix exposed. Give the absolute path to `docs-html/index.html` so it can be opened. Offer
options like *Approve — done* / *Fix a specific page* / *Add more interactivity* / *Regenerate after
I edit a document*. Record the outcome in `00-run-log.md`.
