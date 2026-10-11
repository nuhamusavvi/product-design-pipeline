# Design Brief Template — Stage 13

Written in **English**. Ask the stage-13 questions in `intake-questions.md` first — **question 1 is
the platform confirmation**, and nothing visual is proposed until it is answered.

The brief is a contract: stage 15 implements it literally. Anything vague here becomes a guess
there. Every color gets a hex, every font a name and weight, every spacing a number.

Mark the provenance of each decision: `[client]` (from their brand) or `[defined]` (chosen here).

---

## Platform profiles

§0 of the brief is instantiated from this table. Pick the row matching the confirmed platform and
fill in the concrete values — do not invent a frame size or a navigation pattern.

| Profile | Design frame | Breakpoints | Navigation (RTL) | Input model | Platform specifics |
|---------|--------------|-------------|------------------|-------------|--------------------|
| **Mobile app** | 390×844 (iOS) or 360×800 (Android) | single | Bottom tab bar, rightmost tab = home; full-screen push; bottom sheets | Touch only — targets ≥ 44px, **no hover states** | Safe-area insets, Android system back, no browser chrome, force-update screen |
| **Responsive web** | 1440 primary; 768 and 390 verified | 390 · 768 · 1440 | Top bar + sidebar anchored **right**; dropdown menus; centered modals | Pointer + keyboard + touch — hover **and** `:focus-visible` both required | Browser back, deep links, real page titles, print styles, no splash screen |
| **Both — mobile-first** | Draw at 390, adapt to 1440 | 390 → 768 → 1440 | Tab bar → sidebar · sheet → modal · push → route | Both models supported | Every screen carries a desktop adaptation note |
| **Admin / back-office web** | 1440 primary, 1024 minimum | 1024 · 1440 | Persistent right-anchored sidebar; dense data tables; bulk actions | Pointer + keyboard first; shortcuts expected | Data density over polish; mobile not required unless stated |

The profile is not a suggestion. Stage 14 draws frames at its width; stage 15 renders screens in its
device frame and implements its navigation pattern. A bottom tab bar on an admin profile, or a
hover-only affordance on a mobile profile, is a defect.

---

```markdown
# Design Brief — <Product Name>

Basis: `01-brd.md`, `10-screen-list.md`, platform and brand inputs in `00-run-log.md`.
Provenance: `[client]` = from the client's existing brand · `[defined]` = defined in this brief.

## 0. Platform and viewport

Confirmed at the stage-13 gate. Everything below this section is designed for it, and stages 14
and 15 implement it literally.

| | |
|---|---|
| **Platform** | Mobile app · Responsive web · Both, mobile-first · Admin back-office web |
| **Target devices / OS** | e.g. iOS 15+, Android 9+ / last 2 versions of Chrome and Safari |
| **Design frame** | e.g. 390 × 844 |
| **Breakpoints** | e.g. 390 · 768 · 1440 — or "single, 390" |
| **Navigation pattern** | e.g. bottom tab bar, 4 items, rightmost = home |
| **Input model** | Touch only · Pointer + keyboard · Both |
| **Touch targets** | ≥ 44 × 44px — omit for pointer-only profiles |
| **Hover states** | Required · Not applicable (touch-only) |
| **Chrome allowances** | Safe-area insets top/bottom · browser chrome · none |
| **Screens excluded by platform** | e.g. no splash or permission primers on web |

### Desktop adaptation rules
*(Required when the platform is "Both — mobile-first". Omit otherwise.)*

| Mobile | Becomes on desktop | Applies to |
|--------|--------------------|-----------|
| Bottom tab bar | Persistent sidebar anchored right, 240px | All screens |
| Bottom sheet | Centered modal, max 560px | S-12, S-22 |
| Single-column list | 3-column card grid at 1440, 2 at 768 | S-08, S-15 |
| Full-screen push | Route change with the sidebar persisting | All |
| Full-width CTA | Inline button, auto width, aligned to inline-start | Forms |

Every screen in `14-wireframes.md` carries its own adaptation note; this table holds the global
rules those notes may reference instead of restating.

## 1. Brand Identity

- **Positioning**: one sentence — what this product is, for whom, and what makes it different.
- **Personality**: 3–5 adjectives, each with a one-line UI consequence.
  *e.g. Trustworthy → visible prices and states, no dark patterns, confirmations before commitment.*
- **Voice in Arabic**: formal فصحى, modern standard, or colloquial? Second person مفرد or جمع?
  Address the user as أنت / حضرتك / neutral? Give three sample microcopy lines in Arabic:
  a primary CTA, an error, an empty state. These set the tone for all copy at stage 15.
- **What this brand is not**: two or three explicit rejections.

## 2. Target Audience

- **Primary**: age, role, location, income/context — from the personas in stage 1.
- **Device and context**: phone model tier, screen size, one-handed use, bright sunlight,
  intermittent connectivity, time pressure. Each has a design consequence — name it.
- **Digital literacy**: drives label verbosity, icon-only vs icon+label, onboarding depth.
- **Accessibility needs**: WCAG 2.1 AA minimum — contrast ≥ 4.5:1 body / 3:1 large text and UI
  components, touch targets ≥ 44×44px, text scalable to 200%, never color as the only signal.
- **Cultural notes**: imagery conventions, gender representation, religious or seasonal
  sensitivities, local color associations relevant to this market.

## 3. Visual Style

- **Mood**: 3–5 words + a one-paragraph description of the feeling on first open.
- **Density**: airy / balanced / dense — and why this audience needs it.
- **Shape language**: corner radii scale, whether shapes are soft, sharp, or mixed; any signature
  shape motif (an arch, a slanted cut, a rounded pill) used consistently.
- **Depth**: flat, subtle elevation, or layered. Define shadow tokens if used.
- **Imagery policy**: photography style, illustration style, or icon-only. If illustration:
  line weight, fill style, palette subset. If photography: subject, crop, treatment.
- **Iconography**: family (outline/filled), stroke width, size grid, and which icons mirror in RTL.
- **Motion policy**: duration scale (e.g. 150ms micro / 250ms standard / 400ms page), easing,
  what animates and what never does. Respect `prefers-reduced-motion`.
- **Signature detail**: the one thing someone remembers about this interface.

## 4. Color Palette

| Token | Hex | Role | Usage rule | Provenance |
|-------|-----|------|-----------|------------|
| `--color-primary` | #0F5F4E | Brand, primary CTA | Buttons, active nav, links | [client] |
| `--color-primary-hover` | | Interaction | | [defined] |
| `--color-on-primary` | | Text on primary | | [defined] |
| `--color-secondary` | | Support / accent | ≤ 10% of any screen | |
| `--color-surface` | | Card / sheet background | | |
| `--color-background` | | Page background | | |
| `--color-border` | | Dividers, input borders | | |
| `--color-text` | | Body text | | |
| `--color-text-muted` | | Secondary text, captions | | |
| `--color-success` | | Confirmations | With an icon, never color alone | |
| `--color-warning` | | Caution | | |
| `--color-danger` | | Destructive, errors | | |
| `--color-info` | | Neutral notices | | |

### Contrast verification
| Foreground | Background | Ratio | Passes |
|-----------|-----------|-------|--------|
| `--color-text` | `--color-background` | 12.6:1 | AA / AAA |
| `--color-on-primary` | `--color-primary` | 5.2:1 | AA |

Every text/background pair actually used in the UI must appear here with its computed ratio.

### Theme
Light only / dark only / both. If both, give the dark values in a parallel column — dark is not
an inversion; surfaces lift with lightness, not with shadow.

## 5. Typography

Arabic-capable families only. Give a display face and a body face, with a fallback stack.

| Token | Family | Weight | Size | Line-height | Letter-spacing | Use |
|-------|--------|--------|------|-------------|----------------|-----|
| `--font-display` | "Tajawal" | 700 | — | — | 0 | Headings |
| `--font-body` | "IBM Plex Sans Arabic" | 400/500 | — | — | 0 | Everything else |
| `--text-h1` | display | 700 | 28px | 1.45 | 0 | Screen titles |
| `--text-h2` | display | 700 | 22px | 1.45 | 0 | Section headers |
| `--text-body` | body | 400 | 16px | 1.75 | 0 | Paragraphs |
| `--text-label` | body | 500 | 14px | 1.6 | 0 | Form labels, buttons |
| `--text-caption` | body | 400 | 12px | 1.6 | 0 | Meta, timestamps |

**Arabic typesetting rules**
- Line-height runs higher than Latin — 1.7–1.8 for body, never below 1.45 for headings.
  Arabic ascenders/descenders and diacritics need the room.
- No `letter-spacing` on Arabic — it breaks the connected script.
- No `text-transform` — Arabic has no case.
- No faux bold or faux italic; load the real weights.
- Minimum body size 16px; Arabic loses legibility faster than Latin when small.
- Numerals: **Latin `0-9` always**, including in Arabic copy. One convention, everywhere.

## 6. UI Direction

**Everything in this section is written for the profile confirmed in §0.** Do not hedge with
"mobile or desktop" — pick the one, and specify it concretely.

**And it is written from `13-style-choices.md`, not invented.** The user picked a style per component
at 13b; this section records those picks with their exact metrics and page citations. Pull the
numbers from `assets/style-library-rules.md` — button heights 32/40/48/52/56 with their type sizes,
input heights 40/48, dropdown heights 40/48/56, toggle track 40×24, chip 32, radio row 240×56,
snackbar 420. Cite the page for anything a developer might question, and mark `[inferred]` values as
inferred. Any component the user left unchosen is named in the gate summary, not silently defaulted.

### Grid and spacing
- Base unit: 4px (or 8px). Spacing scale: 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64.
- Screen padding (inline), per §0 breakpoint: state the value at each one you listed.
- Content max-width and column grid — required for web and admin profiles, omit for mobile-only.

### Radii and elevation
- `--radius-sm/md/lg/full` with pixel values.
- `--shadow-1/2/3` with full CSS values, or "flat — no shadows" if that is the direction.

### Component specifications
Define each with: anatomy, sizes, and every state the profile can produce.

**State set by input model** — from §0:
- **Touch-only profile**: default, active/pressed, focus-visible, disabled, loading, error.
  Do **not** specify hover — it does not exist, and designing for it produces affordances that
  never appear.
- **Pointer profile**: all of the above **plus hover**. `:focus-visible` is still mandatory —
  hover is not a substitute, keyboard users exist.

Specify for every profile:
- **Buttons** — primary, secondary, tertiary/ghost, destructive; heights, inline padding, icon
  placement (leading icon sits on the **right** in RTL), full-width rules.
- **Inputs** — label position, height, border, placeholder policy, helper text, error text and
  icon, required marker, RTL caret and alignment (`text-align: start`).
- **Selects, pickers, date/time** — including the calendar convention chosen at stage 0.
- **Cards** — padding, radius, border vs shadow, image ratio, tappable area.
- **Lists and rows** — height, divider style, leading/trailing element placement in RTL,
  chevron direction (points **left** in RTL).
- **Toasts / snackbars / banners** — placement, duration, semantic variants.
- **Skeletons and loaders** — skeletons for content, spinners only for actions.
- **Empty states** — illustration + heading + one line + one action.
- **Badges, chips, tags, avatars, progress** — as the screen list requires.

Specify the variant your profile calls for, and only that one:

| Component | Mobile app | Responsive web / Both | Admin back-office |
|-----------|-----------|----------------------|-------------------|
| **Navigation** | Bottom tab bar — item count, active indicator, badge style, rightmost = home | Top bar + right-anchored sidebar; dropdown menus; mobile drawer below 768 | Persistent right-anchored sidebar with grouped sections; collapsible |
| **Header** | App bar — height, title alignment, back affordance on the **right**, action slots | Top bar — logo, primary nav, search, account menu; sticky behaviour | Top bar — breadcrumbs, global search, environment badge |
| **Overlays** | Bottom sheets — heights, drag handle, backdrop, dismiss | Centered modals — max-width, backdrop, escape and click-outside dismiss | Modals + side drawers for detail-without-navigation |
| **Data display** | Cards and list rows | Cards, list rows, and tables above 768 | Dense tables — row height, sticky header, sort, column resize, bulk-select |
| **Bulk actions** | Not applicable | Optional | Required — selection bar, count, action set, undo |
| **Keyboard** | Not applicable | Tab order and shortcuts for search and dismiss | Full shortcut map — navigate, search, save, new, bulk-select |
| **Touch targets** | ≥ 44 × 44px, mandatory | ≥ 44px on touch, ≥ 32px on pointer | ≥ 32px, density is the priority |

## 7. RTL and Localization Rules

- Document direction is RTL; reading order right → left; visual hierarchy flows from the
  top-right corner.
- Layout is authored with **CSS logical properties only** — no `left` / `right`.
- Mirror: chevrons, arrows, back/forward, progress direction, sliders, carousel swipe,
  drawer origin, text alignment, list item leading/trailing.
- Do not mirror: clock icons, media playback controls, brand logos, checkmarks, images of
  real objects, charts of time-series data (agree the convention and note it here).
- Numbers, phone numbers, prices, and Latin brand names stay LTR inside RTL text — isolate them
  (`unicode-bidi: isolate` / `<bdi>`).
- Currency: <symbol and placement for the target market>. Dates: <format and calendar>.
- **Date and time pickers are the documented exception**: the calendar panel is built in **English
  and rendered `dir="ltr"`** — day headers, month names and digits — even in a fully Arabic product,
  because that is the prevailing convention in Arabic apps and websites. Only the panel; the field
  label, helper text and surrounding form stay Arabic RTL. Record it here so stage 15 does not
  "correct" it back.
- Truncation is by line clamp, never by hard character count — Arabic words vary in width.

## 8. Do / Don't

| Do | Don't |
|----|-------|
| Use `--color-primary` for exactly one primary action per screen | Stack two primary buttons |
| State errors in plain Arabic and say how to fix them | Show raw codes or English strings |
| Keep touch targets ≥ 44px | Rely on icon-only actions without labels for low-literacy users |
| Pair every color signal with an icon or text | Use red/green as the only differentiator |

## 8b. Deviations from the style library

The picks in `13-style-choices.md` are **defaults, not law** — stage 15 may depart from them, but
never silently. Every departure gets a row here and is reported at the gate.

| Component | Picked | Used instead | Why |
|-----------|--------|--------------|-----|
| Search field | 48px height | 56px | Arabic placeholder wraps at 48 |
| Dropdown | v3 pill | v1 rounded | Pill at 56px reads as a button, not a select |

Leave the table present with "no deviations" rather than deleting it — an absent table cannot be
distinguished from an unchecked one.

**Expect real rows.** The book's metrics are Latin-first: a field that fits an English placeholder
often will not fit the Arabic one, and Latin line-heights are too tight for Arabic. Deviations here
are the system working, not failing.

## 9. Design Tokens (implementation-ready)

A `:root` CSS block with every token above, ready to be copied into
`15-ui-designs/tokens.css` at stage 15. Include `--font-*`, `--color-*`, `--space-*`,
`--radius-*`, `--shadow-*`, `--text-*`, and a `[data-theme="dark"]` block if dark is in scope.
```

---

## Font pairing candidates (Arabic-capable, Google Fonts)

Vary the pairing between runs — do not default to the same two every time.

| Family | Character | Good for |
|--------|-----------|----------|
| IBM Plex Sans Arabic | Neutral, technical, excellent legibility | Body text, dense UIs, fintech, admin |
| Tajawal | Geometric, modern, friendly | Consumer apps, headings |
| Almarai | Clean, humanist, very readable | Body text, content-heavy products |
| Noto Kufi Arabic | Kufi, structural, distinctive | Display, headings, institutional |
| Cairo | Warm, rounded, approachable | Consumer, lifestyle, delivery |
| Readex Pro | Contemporary, wide, high clarity | Accessibility-focused, education |
| Alexandria | Soft geometric, contemporary | Startups, premium consumer |
| Rubik | Slightly rounded, informal | Playful, youth-facing |
| Baloo Bhaijaan 2 | Heavy, rounded, playful | Kids, games, bold display only |
| Amiri | Naskh, classical, literary | Editorial, religious, heritage |
| Aref Ruqaa | Ruqaa calligraphic | Display only, never body |
| Marhey / Lalezar | Decorative display | Accents only |

Pair a distinctive display face with a highly legible body face. Do not use a calligraphic or
decorative face for body text. If the client's brand locks a font, use it and pick the counterpart
to complement it.
