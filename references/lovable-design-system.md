# Stage 8 — Lovable Design System Prompt

Write `product-design/NN-slug/01-lovable-design-system-prompt.md` only at this stage, before any
screen prompt.

The whole file is English. It is the prompt the user pastes into Lovable. Do not add an Arabic
preface. Do not call Lovable, and do not say the prompt was executed.

Read `00-analysis-ar.md`. Build the prompt from that analysis and from brand facts the user
actually supplied. Do not reuse a fixed prompt, a style library, or a style picker.

## Brand facts

| Fact | When supplied | When missing |
|---|---|---|
| Logo or other asset | Name it and say how Lovable must use it. Do not claim you inspected a file you did not receive. | Say the asset was not supplied. Tell Lovable to leave a replaceable mark and not invent a logo that looks official. |
| Colors | Quote them. They override any other palette. | Do not invent hex values and call them the brand. Tell Lovable to choose a coherent palette and label it as a design choice, not a client color. |
| Typography preference | Quote it. | Do not name a font and attribute it to the client. |
| Visual direction | Quote it. | Tell Lovable to choose a direction that fits the product and to state that choice so it can be replaced. |

Do not ask a brand questionnaire. Ask one Arabic question only when the user said a brand rule
is locked and the value is missing. Otherwise write the prompt and continue.

## What the English prompt contains

Use these sections when the project needs them. Omit a section that does not apply. Do not copy
an example from another industry into this product.

A. Project identity — name, purpose, audience, platform context, interface language, business context.
B. Brand identity — supplied assets, confirmed colors and type, the user's visual direction, restrictions, and the rule for anything missing.
C. Design tokens — color, text, border, neutral shadow, spacing, radius, type hierarchy, and status colors the screens need. If a value was not given, instruct Lovable to choose it and not present it as approved.
D. Layout and responsive behavior — page structure, width, forms, desktop, tablet, mobile, overflow, and alignment. Add RTL layout only when the analysis confirms it.
E. Shared components — only components named in section 7. Do not add the full example list.
F. Component specifications — for the components the product depends on: structure, spacing, type, states, and responsive behavior. Do not invent pixel sizes the user did not require.
G. Interaction — focus, selected, disabled, loading, form feedback, and navigation. Skip decorative animation.
H. RTL and localization — include this only when the analysis supports a language or direction. Cover direction, alignment, icons, mixed Arabic and Latin text, and number, date, or currency format when those were specified. If language is an open question, say so and forbid assuming RTL.
I. Domain-specific components — patterns that come from this product's workflows, not from a sample industry.
J. Constraints — do not invent business features, pages, brand colors, logos, or inconsistent component variants. Add a constraint only when this project needs it.
K. Consistency — shared tokens and components, the same spacing and type, and the same states on every later screen.

Also state that this prompt establishes the project design system, not one page, and that later
screen prompts will rely on it. Do not include database schema, API paths, or backend
architecture. A field name belongs here only when the screen must show it.

The prompt must stand alone. Lovable will not see `00-analysis-ar.md`.
