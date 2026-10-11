# Arabic RTL HTML Guide — Stage 15

Build the approved wireframes as real, browser-ready screens in Arabic, right-to-left, styled
strictly per `13-design-brief.md`.

## Read §0 of the design brief before writing a line

`13-design-brief.md` §0 names the platform, the design frame, the breakpoints, the navigation
pattern, and the input model — confirmed by the user at the stage-13 gate. Everything below follows
it. What it changes:

| §0 says | Then |
|---------|------|
| **Mobile app** | Build at 390×844 (or 360×800). Bottom tab bar. Touch targets ≥ 44px. **No hover states** — a hover-only affordance is unreachable. Safe-area insets via `env(safe-area-inset-*)`. No `<title>`-driven navigation, no print styles |
| **Responsive web** | Build at 1440 with 768 and 390 verified. Top bar + sidebar anchored right. Hover **and** `:focus-visible` both required. Real `<title>` per screen, browser-back-safe, no splash screen |
| **Both — mobile-first** | Every screen file is genuinely responsive: correct at 390 **and** 1440, implementing that screen's Desktop adaptation note from `14-wireframes.md`. One file per screen, not two |
| **Admin back-office** | Build at 1440, minimum 1024. Persistent right-anchored sidebar. Dense tables with sticky headers. Keyboard shortcuts. Hover on rows expected. Mobile not required unless §0 says so |

Building a web product inside a phone frame, or putting a bottom tab bar on an admin tool, is a
defect no matter how good the visual design is.

## Implement the picked component styles

`13-style-choices.md` records the style the user picked for each component at 13b, and
`13-design-brief.md` §6 turns those into concrete specs. **Build what they picked** — the pill
dropdown, the underlined input, the segmented tabs — with the metrics the brief gives.

Departures are allowed but never silent: every one needs a row in the brief's **§8b Deviations from
the style library** table with a reason. Arabic RTL will produce genuine ones, because the book's
metrics assume Latin. Record them; do not quietly re-decide.

Precedence when the three sources disagree:
1. **Brief §0 platform profile** — confirmed by the user at a gate; wins over everything.
2. **The style picks** — deviate only with a recorded row.
3. **`frontend-design/SKILL.md`** — read this file in the skill repository. It owns composition, motion, and aesthetic quality. Do not invoke `frontend-design` as a registered skill.

**Read `frontend-design/SKILL.md` for aesthetic execution.** It governs typography personality,
composition, motion, and the refusal to produce generic AI-looking UI. The rules in this file are
Arabic/RTL correctness constraints and they **override** any conflicting example there — in
particular, that file's font suggestions are Latin-first; use the Arabic-capable families
named in the design brief instead.

## Stage 15 has three sub-steps, one gate

- **15a — screens.** One standalone `.html` per screen in `10-screen-list.md`. This guide.
- **15b — catalogue.** `index.html`, the gallery: every screen in a device frame, grouped by module.
  This guide, *"`index.html` — the gallery"* below.
- **15c — flow board.** `flow-board.html`, the client-review journey map: screens in flow position
  with labelled arrows, zoomable and clickable. See `references/flow-board-guide.md`.

All three are reported together at the single stage-15 gate. Do not gate between them.

## Output structure

```
15-ui-designs/
  index.html            catalogue — every screen in a device frame, grouped by module, with S-xx ids
  flow-board.html       client-review board — screens in flow position, arrows, zoom, hotspots
  tokens.css            :root variables copied from design brief §9
  base.css              reset, RTL base, typography, shared component classes
  01-splash.html
  02-welcome.html
  03-phone-entry.html
  ...                   one file per screen in 10-screen-list.md, numbered in flow order
  README.md             how to open, screen index, what each state variant demonstrates
```

**One screen, one file.** Never merge screens into a combined document — the whole point is that
`03-phone-entry.html` can be revised in isolation across iterations without touching anything else.
`index.html` and `flow-board.html` reference them by `<iframe>`; they never inline them.

- Every `.html` file is standalone and opens over `file://` with **no build step and no bundler**.
- Fonts come from the Google Fonts CDN with a system Arabic fallback stack, so the pages still
  read correctly offline.
- Only `tokens.css` and `base.css` are shared; screen files link both and add a small
  page-scoped `<style>` block for anything specific to that screen.
- No frameworks. Plain HTML + CSS, with vanilla JS only where a state toggle or tab switch makes
  the screen understandable.

## Non-negotiable RTL rules

### Document
```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
```
Every file. No exceptions, including `index.html`.

### CSS logical properties only

Physical directions are banned. The whole point is that the layout is authored RTL-native rather
than mirrored after the fact.

| Never write | Write instead |
|-------------|---------------|
| `margin-left` / `margin-right` | `margin-inline-start` / `margin-inline-end` |
| `padding-left` / `padding-right` | `padding-inline-start` / `padding-inline-end` |
| `left:` / `right:` | `inset-inline-start:` / `inset-inline-end:` |
| `border-left` / `border-right` | `border-inline-start` / `border-inline-end` |
| `text-align: left` / `right` | `text-align: start` / `end` |
| `border-top-left-radius` | `border-start-start-radius` |
| `float: left` | `float: inline-start` |
| `top` / `bottom` | `inset-block-start` / `inset-block-end` (fine to keep, but be consistent) |

`margin-inline: 16px 8px` and `padding-inline: 16px` shorthands are preferred where they apply.
Flexbox and grid already follow `dir`, so `flex-direction: row` reads right-to-left automatically —
do **not** use `row-reverse` to "fix" it, that double-flips and breaks LTR previews.

Self-check before finishing: grep the output for
`margin-left|margin-right|padding-left|padding-right|border-left|border-right|text-align:\s*(left|right)|float:\s*(left|right)`
and fix every hit.

### Mirroring

| Mirror in RTL | Do not mirror |
|---------------|---------------|
| Back / forward chevrons and arrows | Clock and timer icons |
| Disclosure chevrons in list rows (point left `‹`) | Media playback controls (play still points right) |
| Progress bars and steppers (fill right → left) | Checkmarks, close/X |
| Sliders and range inputs | Brand logos and wordmarks |
| Drawer and sheet entry direction | Photographs of real scenes |
| Carousel swipe direction | Numerals themselves |
| Send / reply icons | Charts of time series (fix a convention and state it) |

Mirror with `transform: scaleX(-1)` on the icon element, never by shipping a second asset.

### Bidirectional text

Numbers, prices, phone numbers, email addresses, URLs, and Latin brand names embedded in Arabic
text must be isolated or they reorder visibly:

```html
<p>رقم الطلب <bdi>#48120</bdi> بقيمة <bdi>120 ر.س</bdi></p>
```
or in CSS: `unicode-bidi: isolate;` on the containing element.

Test case to check in every build: a line containing Arabic + a number + a Latin word, e.g.
`تم الدفع عبر Visa بقيمة 250 ر.س` — the digits and "Visa" must stay in their own left-to-right
runs without the surrounding Arabic breaking apart.

## Arabic typography

- Load the exact families named in design brief §5 from Google Fonts, with `display=swap`.
- Fallback stack: `"<Chosen Family>", "Noto Sans Arabic", "Segoe UI", Tahoma, system-ui, sans-serif`.
- `line-height` ≥ 1.7 for body, ≥ 1.45 for headings. Arabic needs the vertical room.
- `letter-spacing: 0` on all Arabic — never track Arabic text, it severs the connected script.
- No `text-transform` — Arabic has no letter case. Remove it from any copied component CSS.
- No synthetic bold or italic; load the real weights you use and no more than four.
- Minimum body size 16px. Captions no smaller than 12px.
- Do not apply `font-feature-settings` that disable ligatures — Arabic depends on them.

## Content rules

- **Every visible string is Arabic.** Buttons, labels, placeholders, headings, error messages,
  empty states, tab labels, timestamps, tooltips. Zero English in the rendered UI.
- Copy comes from the Arabic copy tables in `14-wireframes.md`. Where a table has a gap, write
  natural Arabic in the voice defined in design brief §1 — do not fall back to English.
- **Realistic placeholder data**, matched to the target market from the run log: real-sounding
  Arabic names (أحمد العتيبي, نورة الحربي), plausible city and district names, believable prices in
  the local currency, sensible dates and times. No lorem ipsum, no "Item 1 / Item 2", no `foo`.
- **Digits are Latin `0-9` throughout, on every screen, including Arabic ones.** Prices, counts,
  dates, badges, percentages, page numbers — all Latin. This is the convention in Arabic apps and
  websites, and it applies even where the surrounding copy is fully Arabic.
- Dates follow the calendar chosen at stage 0.

### The one component that stays English — date and time pickers

**A calendar panel is built in English and rendered LTR, even in a fully Arabic product.** This is
the prevailing convention in Arabic apps and websites and it overrides the "zero English in the
rendered UI" rule above. Applies to the date picker, the date-range picker, and any time picker.

```html
<!-- LTR island inside the RTL page -->
<div class="datepicker" dir="ltr" lang="en">
  <div class="dp-head">Jun <span>2021</span></div>
  <div class="dp-grid">Mo Tu We Th Fr Sa Su … 1 2 3 4 5</div>
</div>
```

| Inside the panel | Outside the panel |
|------------------|-------------------|
| Day headers `Mo Tu We…`, month/year `Jun 2021`, **Latin digits**, range presets `Last 30 days` | The field label, helper text, error text and surrounding form are **Arabic, RTL**, as everywhere else |

- Do **not** mirror the week columns, the `‹ ›` month arrows, or the `→` between range fields —
  they sit in an LTR context and already read correctly.
- The value shown in the closed field is Latin; wrap it in `<bdi>` so it does not reorder the
  Arabic around it.
- Everything else on the screen stays Arabic RTL. The exception is the panel, not the form.
- Currency placement per design brief §7.
- HTML comments may be English (they are for the developer, not the user).

## States

For every screen where `11-states-and-edge-cases.md` defines them, render the meaningful states —
at minimum loading, empty, and error for any screen backed by network data.

Two acceptable patterns; pick one and use it consistently:
1. **Variant files** — `05-search-results.html`, `05-search-results--empty.html`,
   `05-search-results--error.html`, all linked from `index.html`.
2. **In-page state switcher** — one file with a small fixed control (labelled in Arabic) that
   toggles `data-state` on `<body>`, with CSS showing the matching block. Better for review,
   fewer files. If used, the switcher must be visually distinct from the UI itself so it is not
   mistaken for a product feature.

## Responsive behaviour — "Both — mobile-first" profiles only

When §0 says the platform is Both, each screen is **one file that works at both widths**, not two
files. Implement that screen's Desktop adaptation note from `14-wireframes.md`:

- Author mobile-first. Base styles are the 390px layout; `@media (min-width: 768px)` and
  `(min-width: 1440px)` add the adaptations. Never write desktop-first and undo it downward.
- The global transformations (tab bar → sidebar, sheet → modal, push → route, full-width CTA →
  inline button) live in `base.css` so every screen inherits them consistently. Only screen-specific
  reflow goes in the page's `<style>` block.
- Hover states are wrapped in `@media (hover: hover) and (pointer: fine)` so they never activate on
  a touch device and leave a stuck highlight.
- Column reflow uses the counts named in the adaptation note. Do not invent a breakpoint the brief
  did not list.
- Anything mobile-only (pull-to-refresh, swipe actions) needs a visible pointer equivalent above
  768 — a refresh button, a row action menu.

For every other profile, build for the single frame §0 names. Do not add speculative responsiveness
a mobile-only or admin-only product will never use.

## Accessibility

- Contrast pairs must match the verified table in design brief §4.
- Visible `:focus-visible` styling on every interactive element — on every profile. Hover is never a
  substitute; keyboard users exist on web and admin, and switch-control users exist on mobile.
- Real semantic HTML: `<button>`, `<a>`, `<label for>`, `<nav>`, `<main>`, heading hierarchy.
  A `<div>` with a click handler is not a button.
- `aria-label` in Arabic for icon-only controls.
- Touch targets ≥ 44×44px on any profile with touch; ≥ 32px on pointer-only admin profiles.
- **Hover is an enhancement, never the only affordance.** On mobile profiles, do not write hover
  styles at all. On web and admin profiles, every hover-revealed action must also be reachable by
  keyboard and visible on focus.
- `@media (prefers-reduced-motion: reduce)` disabling non-essential animation.
- Never signal state with color alone — pair it with an icon or text.

## Web and admin profiles need these too

Mobile profiles skip this section entirely.

- A real, distinct `<title>` per screen — it is the browser tab and the bookmark.
- Navigation that survives browser back and forward; no state that only exists in memory.
- No splash screen. A web app that shows a branded loading screen before content is a mobile
  pattern misapplied.
- Deep-linkable URLs implied in the markup (even as `href="#"` placeholders with a comment naming
  the intended route), so the frontend team knows the routing shape.
- `@media print` for any screen a user will plausibly print — invoices, bookings, reports.

## `index.html` — the gallery

The review surface. It must:

- Be RTL and Arabic itself (its own chrome, headings, and module labels in Arabic).
- **Frame every screen at the size the platform profile specifies**, rendered live in an `<iframe>`
  so reviewers see the real thing:

  | §0 profile | Frame |
  |------------|-------|
  | Mobile app | Phone frame, 390×844 (or 360×800), with a device bezel |
  | Responsive web | Browser frame, 1440×900, with a simple chrome bar |
  | Admin back-office | Browser frame, 1440×900 |
  | Both — mobile-first | Browser frame at 1440 **plus** a phone/desktop toggle per screen, so a reviewer can check both without leaving the gallery |

- Label each frame with its `S-xx` id and Arabic screen title, and link to the standalone file.
- Group frames by module, in the same order as `10-screen-list.md`.
- Show state variants adjacent to their parent screen, labelled.
- Include a short header stating the product name, **the platform and frame size**, the design
  direction in one line, and the font/palette in use.
- Carry a prominent link to `flow-board.html` — the catalogue answers *"what screens exist"*, the
  board answers *"how does a user move through them"*, and a reviewer usually wants the second.

## `flow-board.html` — the client-review board

Built at **15c**, specified in full in `references/flow-board-guide.md`. Load that guide when you
reach this step. In short: an overview map of flows, drilling into each flow's screens as live
iframes laid out right-to-left with labelled connector arrows; a `عرض` / `تجربة` toggle for static
review versus clickable hotspots; comment pins with markdown export, a legend, per-screen status
badges, and a print layout.

The single most important rule from that guide, repeated here because it is easy to get wrong:
**`file://` is an opaque origin.** The board cannot script into its iframes and cannot `fetch`
anything. Hotspots are the board's own overlay divs positioned in percentages; all data is baked in
at generation time.

## Verification before the final gate

Run through this list and report the result — do not claim done without it:

1. Screen count in `15-ui-designs/` equals the screen count in `10-screen-list.md`. Name any gap.
2. `dir="rtl"` and `lang="ar"` present in every file, including `index.html`.
3. Grep for physical CSS directions — zero hits.
4. Grep the rendered text for `[A-Za-z]{3,}` outside of code, class names, font names, and `<bdi>`
   Latin brand names — any hit is untranslated UI copy.
5. No `lorem`, no `Item 1`, no placeholder gibberish.
6. Every chevron in a list row points left; every back affordance is at the inline-start (right).
7. `index.html` opens in a browser and every iframe and link resolves.
8. Digit convention consistent with the run log across all screens.

### Platform conformance — check against `13-design-brief.md` §0

9. Every screen is built at the frame size §0 specifies. No phone-width web app; no desktop-width
   mobile app.
10. The navigation pattern matches §0 — bottom tab bar only on mobile, right-anchored sidebar on
    web and admin. Grep for a tab-bar class on a web profile: zero hits.
11. **Mobile profiles**: grep for `:hover` — zero hits outside a `@media (hover: hover)` guard.
    Touch targets ≥ 44px. Safe-area insets present.
12. **Web and admin profiles**: every file has a distinct real `<title>`; no splash screen exists;
    hover **and** `:focus-visible` are both styled.
13. **"Both" profiles**: every screen renders correctly at 390 and 1440, implements its Desktop
    adaptation note from `14-wireframes.md`, and wraps hover in `@media (hover: hover)`. Name any
    screen whose adaptation note was not implemented.
14. Screens the platform excludes are absent — no splash or permission primer on a web build, no
    print view on a mobile-only build.

### Style conformance

15. Every component matches the style picked in `13-style-choices.md`, or has a row in the brief's
    §8b deviations table. Name any departure that has no row — that is the check.

### Flow board — 15c

16. Run the ten-point checklist in `references/flow-board-guide.md` §10 and report it alongside
    this one.

## Final gate

Summarize: files produced, screens covered, state variants, **the platform and frame size built
for**, the font pairing and palette used, the flow-board result, and anything you had to decide that
the brief left open.
Give the exact paths to **both** `index.html` and `flow-board.html` so they can be opened — the
board is the one to send a client. Offer options like *Approve — done* / *Revise specific screens* /
*Change the visual direction* / *Add missing states* / *Adjust the board layout*. Record the outcome
in `00-run-log.md`, and update the `## Screen status (stage 15)` table there so the next iteration's
badges are correct.
