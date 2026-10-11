# Style Library Rules — extracted from *Design Cheat Sheets*

Source: `Design Cheat Sheets` bonus, book pages 128–242. Extracted once; consumed by
`style-library.html` (the picker) and by stage 13 when writing `13-design-brief.md`.

**Every rule is tagged:**
- `[stated]` — the book says it in words, or labels it in a measurement callout
- `[inferred]` — read off the artwork; the book never states it

The distinction matters most on pages like *Dropdown Styles* (p.176), where six visually distinct
variants carry no explanatory text at all. Treat `[inferred]` as a reasonable reading, not gospel.

**Latin-first caveat.** The book's metrics assume Latin script. Arabic needs more line-height, no
letter-spacing, and often more field height for the same nominal font size. Every metric below is a
starting point for Arabic RTL, not a final value — see the RTL adaptation notes per component.

---

## FOUNDATIONS

### Spacing scale
`[inferred, from measurement callouts across pp.128–176]`
The book measures in a consistent set: **4 · 8 · 12 · 16 · 20 · 24 · 32 · 40 · 48 · 56 · 64**.
Base unit is **4**, with **8** as the working step and **16 / 24** carrying most component padding.
No callout anywhere uses an odd number or a non-multiple of 4.

### Icon sizing
`[inferred]` Icons are **20px** in small controls, **24px** in medium and large. Never scaled
between those two.

### Icon-to-label gap
`[stated, p.161]` **4px** at small size, **8px** at medium and large.

---

## BUTTONS

### Anatomy `[stated, pp.128–130]`
| Spec | Value |
|---|---|
| Reference width / height | 137 × 40 (label + trailing icon), 117 × 40 (label only), 170 × 40 (leading icon + label) |
| Inline padding | 24 each side |
| Icon box | 24 |
| Icon ↔ label gap | 4 (p.128) |
| Trailing edge padding after icon | 16 (p.128) |

### Sizes `[stated, p.161]`
| Size | Height | Type | Inline padding | Icon gap | Vertical padding |
|------|--------|------|----------------|----------|------------------|
| Small | 32 or 40 | Inter 12 Semibold | 16 | 4 | 20 |
| Medium | 40 or 48 | Inter 14 Semibold | 16 | 8 | 24 |
| Large | 52 or 56 | Inter 16 Semibold | 24 | 8 | 24 |

Each size ships as a pair — the taller of the two is the touch-comfortable variant. `[inferred]`

### Styles — 24 variants `[inferred, pp.128–129]`
The book numbers them 1–24 and says nothing about any of them; all descriptions below are read off
the artwork.

| # | Fill | Shape | Icon | Distinguishing feature |
|---|------|-------|------|------------------------|
| 1 | Gradient | Rounded ~10 | — | Baseline gradient |
| 2 | Gradient | Sharp ~2 | — | Same fill, square corners |
| 3 | Solid | Sharp | — | Hard offset shadow in a contrast hue, bottom + trailing edge |
| 4 | Solid | Rounded | — | Soft diffuse drop shadow |
| 5 | Solid | Rounded | Leading, outline | Line icon |
| 6 | Solid | Rounded | Leading, filled | Filled/colour icon |
| 7 | Solid | Rounded | Trailing chevron | Forward affordance |
| 8 | Tint (pale) | Rounded | Trailing | Coloured text on pale fill |
| 9 | Ghost | Rounded | — | Very faint fill, soft edges |
| 10 | Solid | Sharp | — | Perforated ticket edges on both inline sides |
| 11 | Gradient | Pill | Leading | Fully rounded |
| 12 | Solid | Rounded | Leading, in a darker contained square | Icon has its own container |
| 13 | Gradient | Pill | — | Pill, no icon |
| 14 | Tint + border | Rounded | Trailing | Bordered tint |
| 15 | Outline on white | Rounded | Trailing chevron in a circle | Circled affordance |
| 16 | Solid | Rounded | — | Soft shadow, heavier than 4 |
| 17 | Ghost tint | Rounded | Trailing | No border |
| 18 | None (text) | — | Trailing chevron in a circle | Link-style |
| 19 | Solid | Sharp | Trailing arrow in a circle | — |
| 20 | Outline | Pill | Leading | — |
| 21 | Solid dark | Rounded | — | Deepest value + shadow |
| 22 | White | Rounded | Leading | Elevated card-like, shadow |
| 23 | Tint | Pill | Leading | — |
| 24 | Solid | Sharp | Trailing icon in a **darker split block** | Split button |

### States `[stated, p.130]` — labelled Default · Hover · Press · Disabled · Progress
| State | Primary | Secondary |
|-------|---------|-----------|
| Default | Solid brand fill | Outline, brand border + text, white fill |
| Hover | Lighter / desaturated fill `[inferred]` | Tint fill appears behind the border `[inferred]` |
| Press | Darker, more saturated `[inferred]` | Stronger tint `[inferred]` |
| Disabled | Neutral gray fill, white text | Gray border + gray text `[inferred]` |
| Progress | Spinner **replaces** the leading icon; label stays `[inferred]` | Same |

`[inferred]` The label never disappears in Progress — the spinner takes the icon slot. Worth
copying: it prevents the button changing width mid-action.

**Missing from the book:** no `focus-visible` state anywhere. Add one — keyboard users exist, and
WCAG requires it. Flag as a deliberate addition, not a book rule.

### RTL adaptation
Leading icon sits on the **right**; trailing chevron points **left** and sits on the **left**.
Variant 24's split block moves to the inline-end (left). Arabic labels need ~10% more inline
padding at the same font size `[inferred from Arabic metrics, not from the book]`.

---

## TEXT INPUTS

### Anatomy `[stated, pp.131–132]`
| Spec | p.131 | p.132 |
|---|---|---|
| Field width | 280 | 320 |
| Field height | 40 | 48 |
| Label height | — | 24 |
| Label ↔ field gap | 16 | 8 |
| Inline padding | 16 | 16 |
| Leading icon | 24 | 24 |
| Icon ↔ text gap | — | 8 |
| Text area width | — | 256 |

Two documented heights: **40** (compact) and **48** (comfortable).

### Types — 8 `[stated, p.131 — each is titled]`
1. **Simple text** — label above, leading icon, placeholder
2. **Password** — leading lock, trailing eye-off toggle
3. **Date picker** — leading calendar, `dd/mm/yyyy` placeholder
4. **Search** — leading magnifier, no label
5. **Quantity** — segmented `[ + | value | − ]`
6. **Selection dropdown** — leading flag/icon, trailing chevron
7. **Multiselect** — removable chips inside the field
8. **Card input** — trailing card-brand mark

### Label placement — 8 variants `[inferred, p.132]`
Numbered 1–8, undescribed in the book.

| # | Placement |
|---|-----------|
| 1 | Label above, outlined box |
| 2 | Label inside the box, above the value (filled/stacked) |
| 3 | Label outside on the inline-start, box beside it |
| 4 | Label above, box with a leading icon |
| 5 | Label notched into the top border (Material outlined) |
| 6 | Label above, **underline only** — no box |
| 7 | Label inside, tinted fill + bottom border (Material filled) |
| 8 | Label above, tinted box with a leading icon |

### States — 6 `[stated, p.175 — each is labelled]`
| State | Treatment |
|-------|-----------|
| Default | Neutral border, faint tinted fill |
| Hover | Border shifts to brand hue |
| Typing | Brand border **and brand-coloured label**, visible caret |
| Typed | Border and text darken to full contrast |
| Error | Coral/red border + error message beneath in the same hue |
| Disabled | Gray fill, gray placeholder, border de-emphasised |

`[inferred]` The label changes colour on Typing but not on Typed — focus is signalled by the label,
completion by contrast. A subtle, worthwhile detail.

**Missing:** no separate `focus-visible` ring distinct from Typing; no success/valid state. Add both.

### Famous design-system inputs `[stated, p.169 — each is named]`
Rest / focus pairs from five systems, useful as convention anchors:
1. **iOS 16** — filled, subtle underline, trailing clear `⊗`
2. **Material 3** — notched outline label, trailing clear, supporting text beneath
3. **Fluent (Microsoft)** — thin box, blue focus border
4. **Carbon (IBM)** — label above, filled + bottom border, blue on focus
5. **Ant Design** — box, leading icon, blue focus glow

### RTL adaptation
Leading icon on the **right**, trailing affordance (clear, eye, chevron) on the **left**.
`text-align: start`; caret starts at the right. Arabic placeholders run longer than English — the
40px compact height often needs to become 48. Variant 5's notched label needs the notch on the
inline-start (right).

---

## DROPDOWNS / SELECTS

The book gives dropdowns two separate pages, covering different axes. Both are pickable.

### Axis A — label & icon configuration `[stated, p.170 — each row is titled]`
Four configurations, each at **three heights: 40 / 48 / 56**.

| Configuration | Composition |
|---|---|
| **Lean dropdown** | Value + trailing chevron. No label, no icon |
| **Label only** | Label above the field, value + chevron |
| **Icon only** | Leading icon inside the field, value + chevron, no label above |
| **Icon & label** | Label above **and** leading icon inside |

`[inferred]` All four share: faint tinted fill, hairline border, ~8px radius, 16px inline padding.

### Axis B — visual treatment, 6 variants `[inferred, p.176]`
Numbered 1–6 with no explanatory text. All show label above + leading icon + value + chevron.

| # | Shape | Fill | Chevron | Distinguishing feature |
|---|-------|------|---------|------------------------|
| 1 | Rounded ~10 | Faint tint, hairline border | Thin outline `⌄` | The baseline |
| 2 | Rounded ~6 | Faint tint, border | **Solid filled triangle ▼** | Heavier affordance |
| 3 | **Pill** | Faint tint, border | Solid triangle | Fully rounded |
| 4 | Rounded | Faint tint, border | **Two-way stepper `⌃⌄`** | Signals cycling, not opening — and the leading icon is **filled**, not outline |
| 5 | **Pill** | Faint tint, border | **Chevron inside a circular container** | Leading icon *also* in a circular container — the most decorated variant |
| 6 | Rounded | **Solid gray fill, no border** | Thin outline | Borderless, fill carries the affordance |

`[inferred]` Variant 4 is the only one whose affordance implies a stepper rather than a menu — worth
avoiding unless the control genuinely cycles values. The book does not say this.

### RTL adaptation
Leading icon on the **right**, chevron on the **left**. Chevron glyph is vertical so it does not
mirror. Variant 5's two circular containers sit at opposite inline edges.

---

## SELECTION CONTROLS

### Radio button `[stated, p.134 — states and variants are both labelled]`
**States:** Not active (hollow, neutral ring) · Active (brand ring + filled centre dot) ·
Active alternate (brand ring, no dot) · Disabled (gray, de-emphasised)

**Variants:**
1. **Classic** — control + label
2. **Classic with background** — the whole row takes a tinted fill
3. **Contained + icon** — bordered box, control + label + trailing icon
4. **With illustration** — bordered box, control + label + a full-colour illustration

Spec `[stated]`: row 240 × 56 · inline padding 16 · control 24 · control↔label gap 16 · label 128 ·
gap 8 · trailing icon 32 · trailing padding 16.

`[inferred]` Variants 3 and 4 make the entire card the hit target, not just the control — the right
default for touch.

### Toggle — 8 variants `[inferred, p.135]`
Each shown as an off/on pair. Undescribed in the book.

| # | Track | Knob | Distinguishing feature |
|---|-------|------|------------------------|
| 1 | Pill | Inset, white | Baseline |
| 2 | Pill | **Overhangs the track**, shadowed | Knob larger than the track height |
| 3 | **Thin rail** | Sits on the rail | Minimal, line-like |
| 4 | **Square** | Square | Sharp geometry throughout |
| 5 | Square | Square | **`ON` / `OFF` text inside the track** |
| 6 | Pill | Large, shadowed, overhanging | Heavier version of 2 |
| 7 | Pill | Inset | **`✕` / `✓` icons inside the track** |
| 8 | Pill | Inset, with an inner ring | Dark track when off, brand when on |

Spec `[stated]`: track 40 × 24 · knob 20 · travel 20.

`[inferred]` Variants 5 and 7 are the only two that state their meaning without relying on colour —
worth preferring when the toggle carries a consequential setting.

---

## TABS

### Tabs — 7 variants `[inferred, p.145]`
| # | Treatment of the active tab |
|---|------------------------------|
| 1 | Icon + label inline · brand colour + underline |
| 2 | Icon **above** label · brand colour + underline |
| 3 | Tinted rounded rectangle behind the tab |
| 4 | Solid brand rounded rectangle |
| 5 | **Segmented bordered boxes** — active solid brand, others outlined, edges joined |
| 6 | **Segmented pill on a gray track** — active is a solid brand pill |
| 7 | **Segmented on a gray track** — active is a **white** pill (iOS segmented control) |

Spec `[stated]`: item 112 × 56 · top padding 20 · icon 20 · gap to underline 12 · **0 gap between
items** (they butt together, the underline delimits them).

### Tabs component — 8 scrollable variants `[inferred, p.154]`
A horizontally scrolling row with a leading menu/filter icon button.

| # | Active treatment | Icons |
|---|------------------|-------|
| 1 | Tinted pill | none |
| 2 | Solid brand pill | none |
| 3 | Brand text + **dot beneath** | none |
| 4 | Brand + underline | **above** labels |
| 5 | Tinted pill | inline |
| 6 | Brand + underline | inline |
| 7 | **White raised pill with border** | inline |
| 8 | **White pill overlapping the bar's lower edge** | inline |

`[inferred]` The leading icon button in every variant is a persistent "filter/menu" affordance
separate from the scrolling tabs — a useful pattern for category strips that outgrow the viewport.

### RTL adaptation
Tab order runs **right to left**; the first tab is the rightmost. Underline and pill indicators are
symmetric so they need no mirroring, but the scroll origin must start at the right edge, and
overflow scroll direction reverses.

---

## BOTTOM NAVIGATION

The book spreads this across **four separate sheets — 27 variants in total**. They are not
duplicates: pp.136–137 are dedicated component sheets, p.155 is a study of *active-state
indicators* on one fixed 5-item bar, and p.158 *names* six structural types.

| Sheet | Page | Count | What it varies |
|-------|-----:|------:|----------------|
| Bottom Navigation I | 136 | 8 | Whole-bar compositions, CTA placement, label policy |
| Bottom Navigation II | 137 | 6 | Solid bar, label-only active, overlapping circle, end-CTA, floating |
| Bottom Navigation | 155 | 7 | **Active-state indicator only**, everything else held constant |
| Bottom Navigation Types | 158 | 6 | Named structural types |

### Bottom Navigation I — 8 `[inferred, p.136]`
1. Horizontal tinted pill around a **filled icon + label**; every other item icon-only
2. Top bar on the active item + **circular `+` CTA** at the centre, all items labelled
3. **Dot above the icon, inside the bar**
4. **The bar's top edge rises in a rounded bump** over the active item, with the dot floating clear
   of it; only the active item keeps a label
5. Top bar + **diamond CTA** carrying a transfer glyph
6. Classic — every item labelled, active in brand, no extra marker
7. Icons only, active is a **filled** brand icon
8. Icons only, active icon in a **tinted circle**

### Bottom Navigation II — 6 `[inferred, p.137]`
1. **The entire bar in brand colour**; active is a lighter pill, other icons white
2. **Label alone in a tinted pill with the icon hidden**, plus a top bar
3. **Solid circle rising above the top edge** — no shadow, and the label stays on the same
   baseline as its neighbours
4. Icons only with the **CTA pinned inline at the bar's end**, not the centre
5. **Tinted rectangle** behind a stacked icon + label
6. **Floating bar** detached into a rounded container, with a centre CTA

### Active-state indicators — 7 `[inferred, p.155]`
| Type | Description |
|------|-------------|
| **Classic** | Icon + label per item; active takes brand colour and a filled icon |
| **w/ circle CTA button** | A circular CTA overlaps the bar's top edge at centre |
| **w/ diamond CTA button** | Same, as a rotated square |
| **Floating** | The bar detaches from the screen edge into a rounded container; icons only; active sits in a tinted circle |
| **Active text** | Inactive items are icon-only; the active item expands to icon + label in a tinted pill |
| **Bubble** | The active icon lifts with a dot above it; other items can carry badge dots |

iOS spec `[stated]`: bar width 375 · item 75 · bar height 50 · label **Satoshi 12 Medium** ·
icon↔label gap 7 · icon 24 · home indicator 134 × 5 · bottom safe area 34.

### Active-state indicators — 7 variants `[inferred, p.155]`
1. Filled icon + brand label · 2. **Line above the icon** · 3. **Filled circle behind the icon** ·
4. Brand colour only, no marker · 5. **Tinted pill around icon + label**, others icon-only ·
6. **Solid brand block** behind icon + label · 7. **Notch/pointer above** + icon in a tinted circle

`[inferred]` Variants 5 and 6 change the item's width when active, which shifts its neighbours —
avoid unless the bar has ≤ 4 items.

### RTL adaptation
Item order runs **right to left** — the first tab (usually Home) is the **rightmost**. Centre CTA
variants stay centred. The iOS home indicator is centred and does not mirror.

---

## FEEDBACK — SNACKBARS, TOASTS, TOOLTIPS

### Snackbars `[stated, p.148 — the four semantics are named]`
Four semantics — **Information · Success · Error · Warning** — each shown in two treatments:

- **Tinted** — fill in the semantic hue at low opacity, matching icon and text, trailing **text
  action with a countdown**: `Action(4s)`
- **White card** — white fill with a shadow, coloured icon and text, trailing **circular close with
  a countdown ring**

`[inferred]` Semantic hues: info blue · success green · error coral/red · warning amber.
The countdown is *visible* in both treatments — as a number in one, as a depleting ring in the other.
Worth copying: it tells the user how long they have to act.

Spec `[stated]`: 420 wide · 24 vertical padding · 24 inline padding · icon 24 · icon↔text gap 8 ·
text↔action gap 16 · action 85 · trailing padding 24.

### Snack / Toast — 5 variants `[inferred, p.156]`
| # | Treatment |
|---|-----------|
| 1 | Tinted fill, circular semantic icon, trailing `✕` |
| 2 | **Solid semantic fill**, white text and icon, trailing `✕` |
| 3 | **Solid icon block on the leading edge**, white body alongside |
| 4 | Tinted fill with a **progress bar along the bottom edge** counting down to auto-dismiss |
| 5 | White, **large soft halo behind the icon**, trailing outlined **Action** pill instead of a close |

`[inferred]` Variants 4 and 5 are the only two that give the user something other than "read it and
lose it" — 4 shows the time remaining, 5 offers a recovery action. Prefer them for anything
destructive or undoable.

### Tooltips — 7 variants `[inferred, p.147]`
| # | Treatment |
|---|-----------|
| 1 | Dark navy body, tail arrow |
| 2 | Dark slate body, tail arrow |
| 3 | White body with shadow, tail arrow |
| 4 | Brand-coloured body, tail arrow |
| 5 | **Tinted heading strip above a white body** |
| 6 | **White card** — heading, body, text link + solid button |
| 7 | **Dark card** — heading bar, body, underlined link + light button |

Spec `[stated]`, for the rich card (6/7): 320 × 128 · padding 16 · heading↔body 8 · body↔actions 16 ·
action row 32 · link 80 · link↔button gap 16 · button 75 · trailing padding 16 · link height 24.

`[inferred]` Variants 1–4 are transient hints; 5–7 are dismissible coach-marks with their own
actions. They are different components with different lifecycles — do not treat "tooltip" as one
thing.

### RTL adaptation
Icon leads on the **right**; close and action affordances sit on the **left**. The tooltip tail is
positioned relative to its anchor, so it mirrors with the anchor. Countdown rings deplete
counter-clockwise in RTL `[inferred — the book has no RTL guidance at all]`.

---

## TAGS / CHIPS

### 5 variants, each with a default and selected state `[stated, p.140 — columns are labelled]`
| # | Composition | Selected adds |
|---|-------------|---------------|
| 1 | Text only | — |
| 2 | Leading avatar + text | — |
| 3 | Leading avatar + text | **trailing `✕`** |
| 4 | Text | **leading `✓`** |
| 5 | Leading icon + text | **trailing `✕`** |

`[inferred]` Default is a neutral gray fill with dark text; selected switches to a tinted brand fill
with brand text. Variants 3 and 5 only reveal the remove affordance once selected — the chip is not
removable until it is doing something.

Spec `[stated]`: 152 × 32 · avatar 24 · avatar↔label gap 8 · label↔trailing gap 8 ·
trailing padding 16.

`[inferred]` Chip height 32 pairs with the small button height — they are meant to sit in the same
row without optical mismatch.

### RTL adaptation
Avatar/icon leads on the **right**, `✕` on the **left**. `✓` in variant 4 leads on the right. Chip
rows wrap right-to-left.

---

## SEARCH — 6 variants `[inferred, p.146]`

| # | Composition |
|---|-------------|
| 1 | Leading magnifier + placeholder + **trailing mic** |
| 2 | Placeholder + **trailing solid brand square icon-button** |
| 3 | **Leading hamburger + divider + magnifier** + placeholder |
| 4 | Pill field + **detached circular brand button** outside the field |
| 5 | Placeholder + **trailing solid brand "Search" text button** |
| 6 | **Underline only**, no box — leading magnifier + trailing mic |

Spec `[stated]`: 360 × 48 · inline padding 16 · icons 24 · icon inset 12.

`[inferred]` Variants 2, 4 and 5 imply search is **submitted**, not live-filtered; 1, 3 and 6 imply
as-you-type. Pick to match the actual behaviour — the affordance is a promise.

### RTL adaptation
Magnifier leads on the **right**; mic, submit button and detached button sit on the **left**.

---

## PROGRESS — 8 variants `[inferred, p.138]`

| # | Form | Carries |
|---|------|---------|
| 1 | **Numbered stepper** with connector line | Done = check, current = filled, future = neutral; labels beneath |
| 2 | Linear bar | % beneath |
| 3 | Linear bar with a **draggable knob + tooltip** | % in the tooltip |
| 4 | **Segmented dashes** | Filled vs empty count |
| 5 | **Circular ring** | `2 of 5` inside; step name + next step beside |
| 6 | **Dotted circular spinner** | `25 %` inside; step name + next beside |
| 7 | **Chevron step bar** | Done solid + check, current tinted, future pale |
| 8 | **Inline bar** | `25 %` + status text + **time remaining** |

Spec `[stated]` for variant 5: ring 64 × 64 · inner 40 · ring↔text gap 16 · text block 200 wide ·
two lines at 24 each.

`[inferred]` Variants 5, 6 and 8 name **what is happening** and **what comes next**, not just how
far along. For multi-minute operations that is the difference between a user waiting and a user
leaving. Variants 1 and 7 are for wizards; 2–4 for determinate loads; 6 for indeterminate.

### RTL adaptation
Bars fill **right to left**. Steppers number right to left — step 1 is rightmost. The chevron bar
(7) mirrors: its arrows point **left**. Ring progress sweeps counter-clockwise `[inferred]`.

---

## MENU ICONS — 10 named types `[stated, p.151 — every one is named]`

A naming reference, useful for talking to a client precisely.

| # | Name | Form |
|---|------|------|
| 1 | **Hamburger** | Three equal horizontal lines |
| 2 | **Vegie burger** | Two lines |
| 3 | **Chocolate** | 3 × 3 grid of squares |
| 4 | **Candy box** | 3 × 3 grid of dots |
| 5 | **Kebab** | Three vertical dots |
| 6 | **Fries I** | Three lines, tighter |
| 7 | **Fries II** | Three lines, variant weight |
| 8 | **Stairs** | Staggered lines, descending |
| 9 | **Strawberry** | Lines of varied length |
| 10 | **Meatballs** | Three horizontal dots |

Spec `[stated]`: container 48 × 48, icon 24 × 24 — i.e. **12px padding all round**.

### Icon Menu Types — the fuller page, **with purposes** `[stated, p.167]`

p.167 revisits the same family and **does assign purpose**, grouped into two categories. This
supersedes any assumption that the book only names them.

**Main navigation** *(the book: "for large navigation within the whole interface")*
`Hamburger` · `Vegie` · `Fries` · `Stairs` · `Hot dog` · `Bento` · `Oreos` · `Staris 2`

**Others** *(the book: "special purpose")* — each with its stated use:
| Icon | Form | **Stated purpose** |
|------|------|--------------------|
| **Strawberry** | Lines of decreasing length | **Filtering / Sorting** |
| **List** | Dots with lines beside them | **Sorting** |
| **Meat balls** | Three horizontal dots | **Horizontal menu** |
| **Kebab** | Three vertical dots | **Vertical menu** |

The two pages use slightly different name sets — p.151 has `Vegie burger`, `Chocolate`, `Candy box`,
`Fries I/II`, `Meatballs`; p.167 has `Vegie`, `Bento`, `Oreos`, `Hot dog`, `Staris 2`, `List`. Where
they conflict, **p.167 is the one with purposes**, so prefer its names when talking to a client.

### RTL adaptation
None of these mirror — they are symmetric. Stairs (8) and Strawberry (9) are the exceptions: their
ragged edge should sit on the **inline-start** (right) in RTL.

---

## WEB BREAKPOINTS `[stated, p.159 — all values labelled]`

| Tier | Range |
|------|-------|
| Large desktop screens | **> 1440px** |
| Small desktop devices — **base** | **< 1440px** |
| Tablet devices | **< 1024px** |
| Mobile devices (landscape) | **< 768px** |
| Mobile devices (portrait) | **< 480px** |

**Note the conflict.** The book names small desktop as the **base** — design at 1440 and adapt
downward. Our pipeline designs **mobile-first** for the "Both" platform profile (see
`design-brief-template.md` §0). Where they disagree, the platform profile wins, because it was
confirmed by the client at the stage-13 gate. Record it as a deviation.

---

## GRIDS `[stated — every value is a labelled callout]`

### Desktop app grid — p.171
Viewport **1440 × 1024** · **Navigation panel 240** on the inline-start · content **1200** ·
**Margin 24** each side · **Gutter 16, Stretch** · **Columns: 8** · a *Heading Panel* band spans the
full width above the columns.

### Website base grid — p.174
Viewport **1440 × 1024** · **Margin 104** · **Gutter 16** · **Columns: 12, Stretch**. No side
navigation — the wide margin does the centring.

### iOS app grid — pp.172–173
**Gutter 16, Stretch · Columns: 8**, on 375 × 812 and 360 × 800 frames.

| Grid | Columns | Gutter | Margin | Nav |
|------|--------:|-------:|-------:|-----|
| Desktop app | 8 | 16 | 24 | 240 rail |
| iOS app | 8 | 16 | — | — |
| Website base | **12** | 16 | **104** | — |

`[inferred]` Apps use **8 columns**, marketing sites use **12**. The app grid spends its width on a
navigation rail; the website grid spends it on a 104px margin. That single difference is what makes
one feel like a tool and the other feel like a page.

### RTL adaptation
The navigation panel moves to the **right**. Column order runs right to left, so column 1 is
rightmost — this matters when a spec says "spans columns 1–4".

---

## APPLE DYNAMIC ISLAND — 4 states `[stated, p.166]`

| State | Spec |
|-------|------|
| **Idle** | Pill **122 × 36**, lens 11 × 11, 12 inset from the 390 screen edge |
| **Compact** | **314 × 36**, content 65 leading / 73 trailing, 22 vertical |
| **Expanded (media)** | **366 × 200**, artwork 64 × 64, waveform 24 × 24, progress bar 318 × 22, transport controls 40 × 40 / 33 × 40 / 40 × 40 / 28 × 40, 12 insets |
| **Call** | Avatar 50, action buttons 44, gaps 44 / 12 |

`[inferred]` Only relevant on a mobile-app platform profile with iOS in scope. Include it in a
screen list only if the product has a genuine background activity — playback, a live order, a call.

---

## NAVIGATION RAIL / SIDEBAR

The book gives this three pages — two icon-rail pages and one full sidebar page.

### Icon rail — 7 active-state variants `[inferred, p.165]`
A vertical icon-only rail: logo at top over a divider, seven icon items, a red sign-out at the
bottom, and a badge dot on one item.

| # | Active treatment |
|---|------------------|
| 1 | Brand icon + a small **dot beneath** it |
| 2 | **Tinted rounded square** behind the icon |
| 3 | Brand icon + a **vertical bar on the rail's inline-end edge** |
| 4 | **Filled** brand icon + the label `Home` beneath |
| 5 | **Solid brand rounded block**, white icon |
| 6 | Outline icon + the label in a **solid brand pill** beneath |
| 7 | Tinted rounded square, lighter than #2 |

`[inferred]` Variants 4 and 6 reveal the label only on the active item — the rail stays narrow while
still naming where you are. Variant 3's edge bar is the only one that survives at very narrow widths.

### Expanded rail `[stated, p.168]`
| Spec | Value |
|---|---|
| Rail total width | **224** |
| Content width | 192 |
| Item height | **40** |
| Item gap | 12 |
| Icon | 24 · icon↔label gap 8 · label width 144 |
| Section padding | 24 |
| Logo block | 32 tall, 24 above and below |
| Promo illustration | 160 · promo card 152 · CTA 40 |

Active item is a **solid dark rounded block** spanning the content width.

### Full sidebar — expanded and collapsed `[stated, p.149]`
| Spec | Expanded | Collapsed |
|---|---|---|
| Width | **240** | **80** |
| Item height | 40 | 40 |
| Item gap | 4 | 4 |
| Icon | 20 · gap 12 to label | 20, centred |
| Section heading → first item | 16 | 16 |
| Between sections | 24 | 24 |
| Footer account row | 40 · avatar with 16 padding both sides | avatar only |

Structure: window controls · logo + collapse chevron · grouped sections with headings (`Main`,
`Team`) · items with optional **trailing count badges** (`4`, `9+`, `0`) · promo card (112 image,
12/4/16 text rhythm, 32 button) · account footer with a stepper chevron.

Active item: **tinted fill + brand text + a vertical bar on the inline-end edge** — combining two of
the rail's indicators.

`[inferred]` The collapsed rail keeps the badge dots but loses the counts, so a number that matters
must not live only in a badge. Nothing in the book covers the tooltip that a collapsed rail needs.

### RTL adaptation
The rail sits on the **right**. The active-item edge bar (rail #3, sidebar) moves to the **left**
edge — it marks the boundary with the content area, which is now on the left. Collapse chevrons
point **right** to collapse, left to expand. Trailing badges move to the inline-end (left).

---

## TOP PANELS

### Web desktop — 5 variants `[inferred, p.141]`
| # | Composition |
|---|-------------|
| 1 | Logo + **search field** + gift + bell (badge) + avatar + name + chevron |
| 2 | Logo + page title + **primary "Create New" button** + bell + avatar |
| 3 | Logo │ **collapse toggle** in a grey box + spacer + chat, bell + avatar (ringed) + chevron |
| 4 | Logo │ page title + four muted icons (search, chat, bell, cog) |
| 5 | Logo │ **welcome message** + search field carrying a **mic** + avatar + chevron |

Spec `[stated]`: bar **72** tall · CTA 158 × 40 · icon gaps 32 / 24 / 32 · avatar 40 · avatar-to-edge 40.

### Mobile — 6 variants `[inferred, p.142]`
| # | Composition |
|---|-------------|
| 1 | Logo mark + search + bell + avatar |
| 2 | Logo mark + **circled** icon buttons + avatar |
| 3 | **Welcome text** + hamburger |
| 4 | Avatar (badge) + **centred title** + circled action |
| 5 | **Search field** + hamburger |
| 6 | Grid icon + **centred wordmark** + circled action (badge) |

Spec `[stated]`: search field 272 × 40 · icon buttons 32 · gaps 32 · hamburger glyph 20 within a 32 box.

`[inferred]` Variants 4 and 6 centre the title, which forces the two side slots to be equal width or
the title drifts off-centre. Worth knowing before an Arabic title of different length goes in.

### RTL adaptation
Logo moves to the **right**; account and action icons to the **left**. Centred titles stay centred.
The collapse toggle in web #3 mirrors.

---

## DATE PICKERS

### Single date — 5 states `[stated, p.133 — each is labelled]`
**Placeholder** (`dd/mm/yyyy` + calendar icon + chevron) · **Hover** (brand border) · **Filled**
(date in full contrast) · **Disabled** (gray fill, struck-through eye icon) · **Focused** (brand
border with the calendar panel open beneath).

Open panel: **month dropdown + year dropdown** on the inline-start, `‹ ›` arrows on the inline-end,
`Mo Tu We Th Fr Sa Su` column heads, six-row day grid. Selected day is a **solid brand circle**;
hovered day is an **outlined circle**; overflow days from adjacent months are muted.

Spec `[stated]`: panel **280** wide · header padding 24 · month select 72 · arrows 24 with 24 gap ·
day cell **40 × 40**.

`[inferred]` Month and year are **dropdowns, not just arrows** — jumping a year takes one click
rather than twelve. Worth keeping.

### Date range — 4 states `[inferred, p.160]`
1. Closed — calendar icon + `Select date` + chevron
2. Closed, **focused** — brand border
3. **Open** — the substantial one
4. Closed with the range filled in

The open panel has three parts:
- **Preset list** on the inline-start: `Last 7 days · Last 14 days · Last 30 days · Last 3 months ·
  Last 12 months · Month to date · Quarter to date · Year to date · All time`
- **Two month calendars side by side**, with out-of-month days muted
- **Footer**: start and end date fields with an arrow between, plus `Cancel` and a solid `Set Date`

Range rendering `[inferred]`: start day is a **solid** brand cell, days between take a **tinted**
background, the end day is **outlined** while being chosen.

`[inferred]` The preset list is what makes this usable — most users want "last 30 days", not a
specific range. Do not ship the twin calendars without it.

### RTL adaptation — the exception to every other rule here

**The calendar panel stays in English and stays LTR, even in a fully Arabic interface.**
`[client rule — the book does not address localization]`

This is the prevailing convention in Arabic apps and websites, and it overrides the general
"everything in the UI is Arabic" rule that governs the rest of the package:

| Element | Language / direction |
|---------|----------------------|
| Day-of-week headers | English — `Mo Tu We Th Fr Sa Su` |
| Month and year | English — `Jun 2021` |
| Day numbers | Latin digits |
| Range presets | English — `Last 7 days`, `Month to date` |
| Panel direction | `dir="ltr"` — an LTR island inside the RTL page |
| **Field label beside the picker** | **Arabic** — it is form copy, not part of the picker |
| **Value shown in the closed field** | Latin, wrapped in `<bdi>` so it does not disturb the Arabic around it |

Consequences for implementation:
- Do not mirror the week columns; the first column stays on the left inside the panel.
- Do not mirror the `‹ ›` month arrows — they sit in LTR context, so `›` still means "next".
- The two range calendars order left (earlier month) to right (later), as in LTR.
- The `→` between the range fields stays `→`.
- Everything *outside* the panel — the label, the helper text, the surrounding form — is Arabic RTL
  as normal.

**Calendar system** — Gregorian or Hijri — still comes from the stage-0 intake. A Hijri calendar
keeps the same English/LTR treatment for its month names unless the client says otherwise.

---

## SLIDERS — 8 variants `[inferred, p.139]`

| # | Form |
|---|------|
| 1 | Single thumb between two **icons** (volume pattern) |
| 2 | **Range**, two thumbs, with a value box at each end |
| 3 | `−` / `+` buttons flanking a range, values **beneath** the thumbs |
| 4 | `−` / `+` with **tooltip badges above** each thumb |
| 5 | **Stepped track** with notch dots + a tooltip badge showing `34%` |
| 6 | **Gradient track** with emoji endpoints — a satisfaction scale |
| 7 | `−` / `+` with **tick marks and labels beneath** (`0 · 35 · 70`) |
| 8 | **Waveform scrubber** — played bars solid, remaining muted |

Spec `[stated]`: track **240** · thumb 24 · value box 40 × 40 · box↔track gap 8 · thumb spacing 24.

`[inferred]` Variants 3, 4 and 7 all pair the slider with `−`/`+` buttons — a slider alone is hard to
set precisely on touch, and impossible with a motor impairment. Prefer a paired variant for anything
where the exact value matters.

### RTL adaptation
The track fills **right to left**; the minimum is at the right. `−` and `+` swap sides so `+` stays
in the direction of increase. Waveform playback progresses right to left.

---

## PAGINATION — 4 variants `[inferred, p.143]`

| # | Composition |
|---|-------------|
| 1 | Rows-per-page select · `‹` · `Results 150 – 160 of 1096` · `›` · `Go to:` field |
| 2 | Results text · **`Previous`** · numbered pages (active = solid circle) · **`Next`** · Go to |
| 3 | Results text · `‹` · numbers · `›` · Go to |
| 4 | Rows select · `‹` · `1 … 14 [15] 16 … 110` · `›` — the **ellipsis opens a page dropdown** |

Spec `[stated]`: bar **80** tall · arrow glyph 20 within a 32 button · gaps 16 / 32 / 8 · Go-to field 80.

`[inferred]` Variant 4's clickable ellipsis is the only one that scales past ~20 pages without
either truncating badly or producing a very long row. All four show the **total count**, which is
the thing users actually need.

### RTL adaptation
`‹` `›` mirror — "next" points **left**. Page numbers run right to left, so page 1 is rightmost.
Digits follow the run-log convention.

---

## BREADCRUMB — 5 variants `[inferred, p.144]`

| # | Treatment |
|---|-----------|
| 1 | Folder icons + **underlined links** + `›` separators; last crumb solid brand icon, no underline |
| 2 | **Segmented bar** — rectangular icon+label cells; active is a solid brand cell |
| 3 | Same steps as **overlapping rounded pills**, each with its own drop shadow; active is a solid brand pill |
| 4 | Icons + underlined links + **`/` separators**; last crumb in brand |
| 5 | Links with **dropdown chevrons** + `/` separators + an **ellipsis button** for collapsed middle; opening a chevron reveals sibling pages |

Spec `[stated]`: row 24 · separator glyph 20 · crumb gap 24 · icon 24 · icon↔label gap 8 ·
label↔separator 8.

`[inferred]` Variant 5 is the only one that handles deep hierarchies — the ellipsis collapses the
middle and each chevron offers **siblings**, not just ancestors. That is a genuinely different
capability from the others, which only show the path.

### RTL adaptation
Crumbs run right to left — the root is **rightmost**. `›` becomes `‹`. The `/` separator does not
mirror. Variant 3's pills overlap toward the **left**, so the first step sits on top at the right.

---

## MOBILE HAMBURGER BUTTON — 8 variants `[inferred, p.150]`

Each shown as a **closed/open pair** — the menu glyph and its `✕` counterpart.

| # | Container | Closed glyph | Open glyph |
|---|-----------|--------------|------------|
| 1 | White rounded square | Fries (staggered) | Dark `✕` |
| 2 | **Gradient brand** rounded square | Hamburger, white | Gradient `✕`, white |
| 3 | White **circle** | Vegie, brand | Dark `✕` |
| 4 | White rounded square, shadowed | Stairs | Brand `✕` |
| 5 | White rounded square | Staris 2 | Brand `✕` |
| 6 | **Tinted** rounded square | Fries, brand | White circle with **`⊗`** |
| 7 | **Gradient** rounded square | Stairs, white | Gradient `✕` |
| 8 | **Gradient circle** | Hamburger, white | White circle, dark `✕` |

Spec `[stated]`: container **48 × 48**, glyph **24 × 24** — 12px padding all round.

`[inferred]` The open state is always a `✕` in the same container — the container never changes
shape or position between states, only the glyph. That is what keeps the tap target stable.

---

## SWIPE BUTTON — 8 variants `[inferred, p.153]`

A slide-to-confirm control. Track + draggable knob + centred label.

| # | Track | Knob | Label |
|---|-------|------|-------|
| 1 | Pill, tinted | White circle, cart icon | Muted, centred |
| 2 | **Square**, tinted | White square, arrow | Muted |
| 3 | Pill, tinted | White circle, `»` | Muted |
| 4 | **Solid brand**, square | White square, arrow | White |
| 5 | Pill, **outline only** | No container — bare `⇢` glyph | Muted |
| 6 | Pill, tinted | **Solid brand circle**, hand icon | Muted; **trailing cart icon** marks the destination |
| 7 | Pill, tinted | Solid brand circle, cart | Muted; **trailing `»`** |
| 8 | **Solid brand**, pill | White rounded square, hand icon | White |

Spec `[stated]`: **240 × 56** · padding 12 · internal gap 4 · width fixed, height hug · label fills.

`[inferred]` Variants 6 and 7 mark the **destination** as well as the origin, which is what makes a
swipe discoverable — otherwise the user has to guess how far to drag. Prefer them.

### RTL adaptation
**The knob starts on the right and travels left.** This is the component most likely to be built
backwards: the mental model is "swipe forward", and forward in Arabic is leftward. Arrow and `»`
glyphs mirror to `«`. The trailing destination icon moves to the left edge.

---

## CARDS

### Pricing cards `[stated, p.157 — the annotations are labelled]`
A three-tier row with the middle tier promoted. Named devices:
- **Favour annual billing** — a monthly/annual toggle above the row, with a `25% Discount` chip
- **Show most popular option (anchor point)** — the middle card is raised, filled in brand, and
  carries a `MOST POPULAR` badge
- **Evolving illustrations** — the tier icon grows in complexity across the tiers
- Free / Professional / **`Let's chat!`** — the top tier replaces a price with a contact CTA
- Feature lists with check bullets; the paid tier opens with *"All in the Free plan"*
- CTA per tier: tinted → **white on brand** → neutral `Request Demo`

`[inferred]` The middle card is the only one with a solid fill and a white CTA — the anchor is
carried by contrast, not by size alone.

### Product card `[stated, p.178]`
| Spec | Value |
|---|---|
| Card | **312 × 418** |
| Image area | 280 × 210, inset 16 |
| Overlay badge | 124 wide, inset 32 from the top |
| Title → description | 24 → 8 |
| Description → price row | 32 → 12 |
| Price row → actions | 24 → 16 |
| Primary action | 156 × 40 · icon button 20 within 40 · gap 16 |
| Card padding | 24 bottom |

Composition: overlay badge (`Free shipping`) · image · title · two-line clamped description · price
+ **star rating with numeric score** · `More details` outline button + solid cart icon button.

### Web horizontal card `[stated, p.164]`
| Spec | Value |
|---|---|
| Card | **920 × 320** |
| Image panel | 400 wide · gap 40 to content · content 424 · trailing padding 56 |
| Vertical rhythm | 32 top · name 56 · 24 · role 24 · 16 · "Helping with:" 8 · chips 32 · 24 · divider 24 · buttons 48 · 32 bottom |
| Buttons | 248 primary + 24 gap + 152 secondary |
| Type | Name **Satoshi 40 Bold** · role Satoshi 13 Bold · labels Satoshi 13 Medium · buttons Satoshi 16 Bold |

`[inferred]` The 40px name against 13px supporting text is a 3× jump — the widest type contrast
anywhere in the book. It works because everything else is one size.

### RTL adaptation
Image panel moves to the **right**, content to the left. Star ratings fill right to left. Overlay
badges sit at the inline-start (right). Button order reverses — primary at the inline-start.

---

## SOCIAL LOGIN — 6 variants `[inferred, p.152]`

| # | Form |
|---|------|
| 1 | **Icon only** — circular brand-coloured buttons in a row |
| 2 | Pill buttons, **brand-coloured circular icon** + `Login with …` |
| 3 | **Filled in each provider's brand colour**, white label |
| 4 | Icon only, **rounded-square** white containers |
| 5 | Pill, **monochrome black circular icon** + label |
| 6 | Pill, white, **coloured icon and label matching the provider** |

Spec `[stated]`: **216 × 48** · icon 32 · icon↔label gap 32 · label 152.

`[inferred]` Variants 3 and 6 colour the button by provider, which is what Google's and Apple's
brand guidelines actually require. Variants 1, 4 and 5 are the safest for a crowded screen.

### RTL adaptation
Provider icon leads on the **right**. Provider wordmarks are Latin and must stay LTR — wrap in
`<bdi>`. The Arabic label reads `المتابعة عبر Google`.

---

## COVERAGE LEDGER

Every component page in the book, and how it was extracted. `visual` = the page was rendered and
read; `text` = values taken from the PDF text layer only.

| Book page | Sheet | Extracted |
|----------:|-------|-----------|
| 128 | Button Styles I | visual |
| 129 | Button Styles II | visual |
| 130 | Button States | visual |
| 131 | Types of input | visual |
| 132 | Input Styles – Active | visual |
| 133 | Date Picker | visual |
| 134 | Radio Button | visual |
| 135 | Toggle | visual |
| 136 | Bottom Navigation I | visual — 8 variants |
| 137 | Bottom Navigation II | visual — 6 variants |
| 138 | Progress | visual |
| 139 | Sliders | visual |
| 140 | Tags | visual |
| 141 | Top Panel – Web Desktop | visual |
| 142 | Top Panel – Mobile | visual |
| 143 | Pagination | visual |
| 144 | Breadcrumb | visual |
| 145 | Tabs | visual |
| 146 | Search | visual |
| 147 | Tooltips | visual |
| 148 | Snackbars | visual |
| 149 | Sidebar | visual |
| 150 | Mobile (Hamburger) Menu | visual |
| 151 | Menu Types | visual |
| 152 | Social Media Login | visual |
| 153 | Swipe Button | visual |
| 154 | Tabs Component | visual |
| 155 | Bottom Navigation | visual |
| 156 | Snack / Toast | visual |
| 157 | Pricing Cards | visual |
| 158 | Bottom Navigation Types | visual |
| 159 | Web Breakpoints | visual |
| 160 | Date Range Picker | visual |
| 161 | Button Sizes | visual |
| 162 | UX Research Methods | text — reference, not a component |
| 163 | UI vs UX | text — reference, not a component |
| 164 | Web Horizontal Card | visual |
| 165 | Navigation Rail (icon) | visual |
| 166 | Apple Dynamic Island | visual |
| 167 | Icon Menu Types | visual |
| 168 | Navigation Rail (expanded) | visual |
| 169 | Famous Text Inputs | visual |
| 170 | Dropdown Styles (configurations) | visual |
| 171 | Desktop App Grid | visual |
| 172–173 | iOS App Grid | text |
| 174 | Website Base Grid | visual |
| 175 | Text Field States | visual |
| 176 | Dropdown Styles (treatments) | visual |
| 177–178 | Mobile Top Section · Product Card | visual (178) · text (177) |
| 179 | Hamburger Menu (screen) | text — a screen example, covered by p.150 |
| 180–242 | The twelve teardowns | text — see `archetypes.md` |

**Two pages are deliberately not components**: *UX Research Methods* (p.162) classifies methods on
behavioural/attitudinal × qualitative/quantitative axes, and *UI vs UX* (p.163) splits the two
disciplines. Useful framing, nothing to pick.

---

## WHAT THE BOOK DOES NOT COVER

Recorded so stage 13 does not assume silence means "no opinion":

- **No `focus-visible` state** on any component. We add one everywhere; WCAG requires it.
- **No RTL guidance at all.** Every mirroring note above is ours.
- **No dark theme.** Only the teardowns' own dark screens hint at it.
- **No motion or duration specs.** Nothing on easing, transition length, or reduced-motion.
- **No accessibility contrast pairs.** The palettes are shown, never verified.
- **No responsive behaviour per component** — breakpoints are given, adaptation is not.
- **No empty, loading, or skeleton states** for lists and cards.

These gaps are filled by `13-design-brief.md` and by the pipeline's own standards, not by the book.
