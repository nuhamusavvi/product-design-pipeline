# Flow Board Guide — Stage 15c

Build `15-ui-designs/flow-board.html`: a single self-contained file the client can open and see the
whole product as a journey — every screen in flow position, arrows between them, zoomable, and
clickable like a prototype.

This is **not** the catalogue. `index.html` answers *"what screens exist"*, grouped by module. The
board answers *"how does a user move through them"*. Clients ask the second question; both files
ship.

Read `13-design-brief.md` §0 first — the platform profile decides the frame size the board draws.

---

## 1. The constraint that shapes everything: `file://` is an opaque origin

Browsers treat every `file://` document as its own opaque origin. The board **cannot read or script
into its own iframes** — `iframe.contentDocument` throws a `SecurityError`, and `fetch()` of a local
file is blocked outright.

Consequences, all non-negotiable:

- **Hotspots are the board's own DOM**, absolutely positioned *over* each iframe. Never injected
  listeners, never `postMessage` handshakes with the screen files.
- **Nothing is loaded at runtime.** Screen titles, statuses, flow structure, hotspot coordinates —
  all baked into the HTML at generation time. No JSON sidecar, no `fetch`.
- **The board never detects what happened inside a screen.** It only knows what the client clicked
  on its own overlay.

This fails silently when tested behind a local server and breaks the moment the client double-clicks
the file. Build it right the first time.

## 2. Chrome and language

- The board is **Arabic and `dir="rtl"`** — the audience is the Arabic-speaking client. Toolbar
  labels, legend, flow names, arrow labels, comment UI: all Arabic.
- Its chrome uses the **house documentation palette** from `html-docs-guide.md` §1 — ivory
  `#FAF9F5`, slate `#141413`, clay `#D97757`, olive `#788C5D`, rust `#B04A3F`, the gray ramp. The
  board is a tool wrapping the product; the same two-palette rule applies. Product colors live
  inside the iframes, where they belong, and the neutral chrome keeps them looking like the product
  rather than competing with it.
- Serif for headings, system sans for body, mono for ids and metadata. No web fonts for the chrome;
  the screens load their own.
- One file. No shared CSS, no shared JS, no framework, no CDN — the client receives one attachment
  and it works.
- **All numerals are Latin `0-9`**, even inside Arabic labels — screen counts, status roll-ups,
  pin numbers, trigger labels. Never Arabic-Indic. This matches the product screens themselves.

## 3. Level 1 — the overview map

The landing view. Flows as blocks on a pan/zoom canvas.

Each `F-xx` block carries:
- Flow id and Arabic flow name (`F-01 · التسجيل والتحقق`)
- Screen count and entry point (`6 شاشات · من تثبيت التطبيق`)
- A strip of three or four **static silhouettes** — simple CSS wireframe shapes, not iframes. The
  overview must stay light; live screens belong at level 2.
- A status roll-up (`3 محدّث · 1 جديد`) using the badge colors from §8.
- The actor, when flows belong to different roles.

Between blocks, draw **cross-flow arrows** — where one flow hands off to another (`F-01` sign-up →
`F-02` browse, `F-03` checkout → `F-05` order tracking). Take them from the exit-point and
cross-role-handoff rows in `09-user-flows.md`.

Clicking a block drills into level 2. Deep-linkable: `flow-board.html#F-02` opens straight into that
flow, so you can send a client a link to one journey.

## 4. Level 2 — the flow detail

That flow's screens as **live iframes** at the frame size from brief §0, laid out **right to left**
in flow order — the Arabic reading direction, matching the product itself.

| Profile | Frame on the board |
|---------|--------------------|
| Mobile app | Phone bezel, 390×844 (or 360×800) |
| Responsive web | Browser frame with a chrome bar, 1440×900 |
| Admin back-office | Browser frame, 1440×900 |
| Both — mobile-first | Phone frames by default, with a per-board `جوال / سطح المكتب` toggle that reloads every frame at the other width |

Each frame is labelled beneath with its `S-xx` id, Arabic screen title, and status badge.

**Connectors** use the inline-SVG recipe already written in `html-docs-guide.md` §9 — the same three
`<marker>` arrowheads:

| Path | Stroke | Marker |
|------|--------|--------|
| Normal | `--gray-500` | `#arrow` |
| Failure branch | `--rust` | `#arrow-rust` |
| Success terminal | `--olive` | `#arrow-olive` |

Edges run from the source frame's inline-start edge to the target's inline-end edge, cubic-curved
when they change row. Every edge carries an **Arabic trigger label** naming what causes the
transition — `اضغط متابعة`, `رمز صحيح`, `5 محاولات خاطئة`, `انتهت الصلاحية` — set on a small ivory
`<rect>` so the line does not strike through the text.

**Draw the failure branches.** A board showing only the happy path tells the client the product has
no error states, and they will be surprised later. Every decision row and every failure-path row in
`09-user-flows.md` becomes an edge.

Controls: back to overview, previous flow, next flow.

## 5. Canvas mechanics

- **Pan**: drag empty canvas. **Zoom**: ctrl+wheel, `＋` / `－` buttons, `⛶` fit-to-view, and `1:1`.
- Implement as `transform: translate(x,y) scale(z)` on a single `#canvas` wrapper. The SVG arrow
  layer lives **inside** that wrapper so arrows transform with the frames — never transform them
  separately, they will drift.
- **Lazy iframe loading via `IntersectionObserver` is mandatory.** Forty live iframes mounted at once
  will make the page crawl on a client's laptop. Until a screen is near the viewport it shows a
  placeholder card — `S-xx` id, Arabic title, skeleton bars. Unload frames that move far off-canvas
  and restore the placeholder.
- A **minimap** in the corner showing the whole board with the current viewport rectangle; clicking
  it jumps.
- Zoom clamped to a sensible range (roughly 0.15 to 1.5). Below ~0.35 the Arabic in the frames is
  unreadable, so swap frames for their placeholder cards at low zoom — it reads better *and* it is
  faster.

## 6. The two modes

A toolbar toggle, defaulting to `عرض`.

| Mode | Arrows | Hotspots | Clicking a screen |
|------|:------:|:--------:|-------------------|
| **`عرض`** (view) | Visible, with labels | Inert | Opens it full-size at 1:1 in an overlay, with previous/next and the screen's `S-xx` id |
| **`تجربة`** (try) | Hidden | Active | Navigates — pans and zooms to the destination frame and flashes its border |

`تجربة` keeps a **breadcrumb** of the path taken (`الرئيسية ← البحث ← تفاصيل الخدمة`) and a `البداية`
reset. A hotspot whose destination sits in another flow drills across and appends to the breadcrumb,
so a client can walk the real journey end to end.

## 7. Hotspots

- One per navigating action in the screen's annotation list in `14-wireframes.md` — those are marked
  there with `→ S-07`, so targets are authored at stage 14, not guessed here.
- Written as data attributes on a transparent `<div>` layered over the frame:

```html
<div class="hotspot" data-x="8%" data-y="82%" data-w="84%" data-h="7%"
     data-to="S-07" data-label="اضغط متابعة"></div>
```

- **Percentages, always.** A frame-size change — or the `جوال / سطح المكتب` toggle — must not move
  the hotspots off their targets.
- Invisible in `عرض`. In `تجربة` they take a soft clay outline on hover with the Arabic label as a
  tooltip.
- A `تلميح` toolbar button flashes every hotspot at once, for the client who cannot find where to
  click. Assume they will not ask.

## 8. Review tools

### Comment pins
A `💬` tool. With it active, clicking anywhere drops a numbered pin and opens a small textarea.

- Stored in `localStorage`, keyed by run folder plus pin coordinates, so notes survive a reload and
  the client can review across sessions.
- Pins anchored to a screen record its `S-xx`; pins on empty canvas record the flow.
- A side panel lists every comment grouped by screen, with a count badge in the toolbar.
- **`تصدير الملاحظات`** copies a markdown list to the clipboard:

```
- [S-04 رمز التحقق] ملاحظة 3: زر إعادة الإرسال صغير جدًا
- [S-08 نتائج البحث] ملاحظة 4: نحتاج فلتر بالسعر
```

That paste-back is the whole point — it is what closes the loop into the next iteration.

### Legend
A fixed, collapsible panel in Arabic covering: what each arrow color means, what each status badge
means, and how to pan and zoom. Clients who have never opened a design tool need this and will not
ask for it.

### Status badges
Each screen carries one of `جديد` · `محدّث` · `قيد المراجعة` · `معتمد`, colored olive / clay / info /
gray. Baked into the HTML at generation time — `file://` blocks `fetch`, so nothing loads at runtime.

Source: the `## Screen status (stage 15)` table in `00-run-log.md`.

**On a re-run, recompute.** Compare the current screen files against the previous iteration and mark
what actually changed. Do not carry last round's badges forward — a board where everything still
says `محدّث` from three rounds ago is worse than no badges, because the client stops trusting it.

### Print / PDF
`@media print`:
- Page 1: the overview map.
- Then one flow per page — screens as **static scaled frames with a numbered arrow list beneath**.
  SVG connectors do not survive pagination reliably, so the list carries the transitions instead.
- Final pages: the comments appendix.
- Toolbar, minimap, hotspots, and the legend panel hidden.

## 9. Accessibility and fallback

- Every frame is focusable (`tabindex="0"`) and opens with Enter — a client navigating by keyboard
  must not be stranded.
- Beneath the canvas, the same flow order as a plain **ordered list** of screens with their
  transitions, so the board is never the only route to the information. It also gives the print
  layout something reliable to fall back to.
- `@media (prefers-reduced-motion: reduce)` disables pan/zoom easing and the flash animation.
- Arrow meaning is never carried by color alone — the trigger label always says what the edge is.

## 10. Verification before the stage-15 gate

1. Frame count on the board equals the screen count in `10-screen-list.md`. Name any gap.
2. Every `F-xx` in `09-user-flows.md` has an overview block and a level-2 detail view.
3. Every arrow's trigger label traces to a decision or failure row in `09-user-flows.md`.
4. Every hotspot's `data-to` names a screen file that exists in `15-ui-designs/`.
5. Every hotspot coordinate is a percentage — grep for `px` inside `data-x|data-y|data-w|data-h`:
   zero hits.
6. The board opens over `file://` with an empty console. No `contentDocument`, no `fetch`,
   no `postMessage` in the source.
7. Lazy loading actually defers — the network panel shows iframes loading as you scroll, not all
   at once on load.
8. A comment pin survives a reload and exports as markdown.
9. Print preview paginates one flow per page.
10. `dir="rtl"` and `lang="ar"`; no English in the chrome.

Report the results with the rest of stage 15 at its single gate.
