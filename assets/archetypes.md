# Archetypes — the twelve screen teardowns, distilled

Source: *Design Cheat Sheets*, book pp.177–242. Each app is analysed there across four pages —
*Spacing System · Typography Styles · Color Styles · UX Explanation*.

These are **not** variants to pick between like a dropdown style. They are worked examples. At
stage 13 the user may pick one as a *"feel like this"* reference, which seeds the design brief's
density, palette size, and type rhythm. The brief still owns the concept.

Palettes and type specs below are `[stated]` — lifted from the book's own annotations. Character
descriptions are `[inferred]`.

---

## The cross-cutting patterns

Worth more than any single archetype, because these hold across all twelve.

### Palette size
**6 to 15 colours, median 9.** Not 30. Every teardown works with under a dozen values including
white, and the tightest (AirBnb, 6) is the most recognisable. `[stated — counted from the annotations]`

`[inferred]` The composition is consistently: 1 brand, 1–2 accents, 3–4 neutrals, 1–2 semantic,
plus white. Where a palette runs long it is because it carries **two** accent hues for data
(Fintech's mint/coral, Crypto's green/red for gain/loss), not because it has more greys.

### Type scale
**One family, 4–5 sizes.** The sizes cluster hard: **10 · 11 · 12 · 13 · 14 · 16 · 18** with a
display size at **24 · 26 · 32** where a headline or a figure needs it. `[stated]`

`[inferred]` Where a second family appears it is *only* for micro-labels — Fintech pairs Red Hat
Display with Montserrat, Messaging pairs Ubuntu with **Inter 10**, Dovee pairs Manrope with
**Inter 10**. The pattern is: humanist family for content, neutral grotesque for tiny numeric or
metadata text. Never two families at the same size.

### Spacing
`24` and `16` carry almost everything, with `12` and `8` for tight groupings and `4` for
optical nudges. `32 / 40 / 44 / 48` appear as section separation. `44` recurs as the top-bar height
below the status bar. `[stated — counted from the annotations]`

### Density signature
The ratio of `24`-uses to `16`-uses is a good proxy for how airy a screen feels:
airy screens lean on `24`, dense screens lean on `16`.

---

## The twelve

### Checkout — *transactional, calm*
`[stated]` 10 colours · Satoshi 14 · dominant spacing 12 · 16 · 24 · 40
`#1A374D #162F43 #406882 #6998AB #9CB1BA #C9E2FA #3A90DF #474B71 #000000 #FFFFFF`

`[inferred]` A single desaturated navy family with one brighter blue for the action. Balanced
density — `12` and `16` tie as often as `24`. Reads trustworthy rather than exciting, which is
correct for a payment screen. **Take this when money changes hands.**

### Crypto Wallet — *dark, data-forward*
`[stated]` 8 colours · Karla 12/13/16/32 · dominant 24 · 12 · 16 · 48
`#06080E #13141D #232530 #FFFFFF #7BF896 #4EB4FF #FA6666 #9364F5`

`[inferred]` Dark ground with a **mint green for gain and coral for loss** — semantic colour doing
real work, not decoration. The 32px figure is the hero; everything else is 12–16. **Take this for
anything where a number is the point.**

### Music & Podcast — *dark, immersive*
`[stated]` 8 colours · Montserrat 12/14/16 · dominant 24 · 12 · 8
`#111D25 #1D2930 #E5FFFF #CFD2D3 #BBBEC1 #7ED1FF #FA6666 #FFFFFF`

`[inferred]` Near-black with a pale cyan tint as the text colour rather than pure white — softer on
the eye for long sessions. Tight `8`/`12` groupings inside cards, `24` between sections. **Take this
for media browsing.**

### Login — *institutional, spacious*
`[stated]` 9 colours · Satoshi 12/14/16/18 · dominant **24 (×12)** · 16 · 8
`#1A374D #162F43 #406882 #9CB1BA #ADCBD7 #C9E2FA #E9F0F2 #2D8AE0 #7D51D9`

`[inferred]` The most `24`-dominant screen in the book — very airy. Same navy family as Checkout.
Four type sizes only. **Take this for auth and onboarding.**

### AirBnb Explore — *editorial, minimal palette*
`[stated]` **6 colours** · Cereal 10/12/14/16 · dominant 24 · 12 · 32
`#222222 #5C5C5C #737373 #DADADA #FFFFFF #FF5A5F`

`[inferred]` The tightest palette in the book: greys plus one signature red. All hierarchy comes
from type size and weight, none from colour. **Take this when the content is photography and the UI
should disappear.**

### Job Search — *card-based, balanced*
`[stated]` 12 colours · Red Hat Display 10/12/14/16/24 · dominant **16 (×13)** · 12 · 24
`#1B2932 #2C404E #425B6C #4D5A64 #5C849E #5D7B90 #6A899E #C8E0E9 #DAE2FE #EDF6F9 #FFE8D2 #F46C6C`

`[inferred]` `16`-dominant, so denser than Login — cards packed with metadata. Two pale accent
tints (`#FFE8D2` peach, `#DAE2FE` periwinkle) to differentiate card categories without colour-coding
text. Five type sizes, the widest range in the book. **Take this for browse-and-filter lists.**

### Fintech — *dense, dual-accent, two families*
`[stated]` **15 colours** · Red Hat Display 11/12/14/16 + **Montserrat 11/16/26** · dominant 24 · 12
`#112025 #172E35 #1C2B30 #27363B #526366 #ACBFBF #BFD2D1 #BFD4D4 #D4E9E6 #EAFFFC #84F3F3 #92FF96 #F4634F #FFAB9F #FFFFFF`

`[inferred]` The busiest palette, and it earns it: a deep teal ground, two mint accents, and a
coral pair for negative values. The only teardown with a genuine **two-family pairing** — Montserrat
for figures, Red Hat Display for labels. **Take this for dashboards carrying many simultaneous
numbers.**

### Messaging — *bright, conversational*
`[stated]` 12 colours · Ubuntu 12/14/16 + **Inter 10** · dominant **16 (×10)** · 12 · 8
`#0C284F #2A2E3F #52576B #707588 #8A94BA #EBF2F4 #EBF4FF #FFFFFF #2895FB #2856FB #3D65FF #38CA46`

`[inferred]` Three closely-related blues doing different jobs (link, primary, active) plus a green
for presence. `Inter 10` handles timestamps only. Dense `8`/`12` inside message rows. **Take this
for chat and social.**

### Sign-In — *deep indigo, generous*
`[stated]` 13 colours · Manrope 12/13/14/16/18 · dominant 24 · 16 · 32 · 48
`#101A2F #25255A #3D3D74 #585F9D #8A9CB4 #CFDBEC #ECF3FF #F5F9FF #FFFFFF #4255FE #4356FF #428DFE #000000`

`[inferred]` A five-step indigo ramp — unusually many neutrals, all tinted rather than grey, which
is what makes it feel considered rather than default. Five type sizes at close intervals.
**Take this when the brand is a colour rather than a hue family.**

### Tickets Booking — *bold, high-contrast accents*
`[stated]` 8 colours · dominant 32 · 20 · 12
`#1D203B #484B63 #646996 #989BAF #FFFFFF #FF6969 #D6F14E #6142F5`

`[inferred]` The most aggressive accent set in the book — coral, **acid lime**, and violet against
a deep navy-purple. `32` is the dominant step, the loosest in the collection. Built for imagery and
event posters to sit inside. **Take this when the product should feel like an event.**

### Blog — *reading-first*
`[stated]` 8 colours · Montserrat 10/11/12/14/16 · dominant **24 (×13)** · 16 · 20 · 32
`#000000 #1A1C36 #414556 #5A5D7E #696E83 #FFFFFF #2895FB #2856FB`

`[inferred]` Five sizes but none above 16 — hierarchy comes from weight and colour, not scale, which
keeps long text calm. Very `24`-heavy. **Take this for content-heavy reading.**

### Dovee desktop — *dense admin, sidebar-led*
`[stated]` 9 colours · Manrope 12/13/18 + **Inter 10** · dominant **4 (×13) · 16 (×11) · 40 (×11)**
`#0C0E19 #1C2035 #303651 #697089 #868DA5 #E6E8F0 #FFFFFF #556DF5 #E86565`

`[inferred]` The only desktop teardown, and the only one where `4` is the most-used value — dense,
because it is an operator tool with a persistent sidebar. `40` recurs as the sidebar row height.
Three type sizes plus Inter 10 for counts and badges. **Take this for any back-office panel.**

---

## Picking one at stage 13

The archetype seeds three things, and only these three:
1. **Palette size and composition** — how many colours, and how many are accents.
2. **Type rhythm** — how many sizes, how far apart, one family or two.
3. **Density** — which spacing step dominates.

It does **not** dictate the hues, the fonts, or the layout. A client whose brand is green picking
"Fintech" gets Fintech's *structure* — deep ground, dual accents for data, dense `24`/`12` rhythm —
in their green, not in Fintech's teal.

Record the choice in `13-design-brief.md` §3 alongside the mood, and note anything taken from the
archetype that the brand inputs would otherwise have decided differently.
