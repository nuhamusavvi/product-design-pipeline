# Intake Questions

Two question sets: stage 0 (scope and audience) and stage 13 (brand inputs). Ask them with
`AskQuestion` when that tool is available, at most 4 questions per call. If `AskQuestion` is not
available, ask the same questions in chat and wait. Do not invent a tool name or continue as if
they were answered.

## The rule that makes this fast

**Do not ask what the Arabic source already answers.** Read it first, extract everything you can,
then ask only about the gaps. For anything the source implies but does not state outright, put it
in the question as a pre-filled recommended option: *"Roles: customer + admin (Recommended — this
is what the source implies)"*. The user confirms with one click instead of typing.

Aim for two question rounds at stage 0: the four that most change the output, then a
follow-up round if the answers open new gaps. If the source is unusually complete, one call is fine.

---

## Stage 0 — scope and audience

Two tiers. The first is non-negotiable; the second is where you spend the remaining question slots.

---

### ALWAYS ASK — never skip these

#### 1. Product identity
- What is the product called, and what does it do in one line? (Needed for the folder slug.)
- Who is the client — a startup, an existing business digitizing a process, an internal tool?

#### 2. Platform — **mandatory**

**Is this a mobile application, a web application, or both?** Ask it every single run, even when the
Arabic source seems to imply an answer. Implication is not confirmation.

This one answer fixes the design frame, the navigation pattern, the breakpoints, the input model, and
which screens exist at all. Getting it wrong means stage 14 draws a bottom tab bar for a desktop
admin tool, and stage 15 renders a web app inside a 390px phone frame. Getting it *unasked* means
nobody notices until the client does.

Offer the four profiles from `design-brief-template.md` §Platform profiles:

| Option | What it means |
|--------|---------------|
| **Mobile app** | Native iOS/Android. Design frame 390×844 or 360×800, bottom tab bar, touch only |
| **Responsive web** | Browser-first. Design frame 1440, right-anchored sidebar, pointer + keyboard + touch |
| **Both — mobile-first** | Drawn at phone width, every screen carrying desktop adaptation rules |
| **Admin / back-office web** | Dense desktop tool. 1440 primary, persistent sidebar, keyboard-first |

Follow-ups, asked only when the answer makes them relevant:
- **If mobile**: iOS, Android, or both — and does that change anything in the design (Material vs
  Cupertino conventions, system back button, safe areas)?
- **If web or both**: is there a minimum supported width, and does anything need to print?
- **If any customer-facing profile**: is there *also* an admin/back-office panel in scope? Admin
  screens usually belong in their own run — confirm which this one covers.

The answer is re-confirmed at stage 13 before any visual work begins, so a wrong answer here is
recoverable. An **unasked** one is not — it silently becomes an assumption twelve stages deep.

Record the platform, the design frame, the breakpoints, and the navigation pattern in
`00-run-log.md`. Stages 13, 14, and 15 all read them.

---

### ASK IF THE SOURCE LEAVES IT OPEN

Pull from this pool; ask the ones that matter most for this particular product.

### Users and roles
- Which roles exist, and which are in scope for this pass? (Customer, vendor, driver, admin,
  support, moderator …)
- Is there a role that only ever uses a back-office panel? Those screens are usually a separate run.
- Rough digital literacy of the primary user — this drives density and hand-holding in the UI.

### Scope depth
- MVP or full product? MVP means the shortest path to the core value; full means every secondary
  flow gets screens too.
- Anything explicitly out of scope that I should record so it does not creep back in?

### Locale and content
- Primary market/country (drives currency, address format, phone format, calendar).
- UI language: Arabic only, or Arabic plus an English locale? (Default: Arabic only, RTL.)
- *(Not asked — digits are always Latin `0-9`, including in Arabic interfaces.)*
- Calendar: Gregorian, Hijri, or both?

### Integrations that create screens
- Payments (which gateway — this creates checkout and 3DS screens)
- Maps / location / live tracking
- SMS or WhatsApp OTP, or social/national-ID login
- Notifications (push, in-app inbox)
- File/document upload or verification
- Chat or support
- Anything requiring a third-party redirect

### Constraints
- Is there an existing backend or API that fixes the data model?
- Deadline or scope pressure that should shape the MVP cut?
- Regulatory or compliance requirements (health data, KYC, VAT invoicing, accessibility)?
- Any accessibility target (WCAG AA is the default assumption).

### Engineering inputs — needed for stages 5 to 7

Ask these only when the source leaves them open; otherwise propose a default and confirm it at the
stage-5 gate rather than spending a question here.

- **Scale**: expected users and transactions at launch and at year 1. Without a number, `05-srs.md`
  cannot write a testable `NFR-xx`, and the gate will reject it.
- **Availability expectation**: is this a business-hours tool or does it need 24/7 uptime?
- **Existing stack or team preference** that constrains the data model or API shape.
- **Auth model**: phone OTP, email/password, social, national ID, or SSO — this drives half of
  `04-permission-matrix.md` and the first epic in `08-user-stories.md`.
- **Data residency or retention** rules imposed by the client or the regulator.
- **Who receives the handoff**: an in-house team, an agency, or a team not yet hired. This changes
  how much explanation `05-srs.md` and `07-api-surface.md` need to carry.

### Example call

Platform occupies slot 1 in the first batch. Always.

```
Q1 "Platform"      — Mobile app (iOS+Android) / Responsive web / Both, mobile-first /
                     Admin back-office web
Q2 "Roles in scope" [multiSelect] — Customer / Vendor / Driver / Admin
Q3 "Scope depth"   — MVP core flows (Recommended) / Full product / Core + admin
Q4 "Locale"        — Arabic only (Recommended) / Arabic + English /
                     Arabic + Hijri dates / Arabic + Gregorian only
```

Record every answer in the `## Intake answers` table of `00-run-log.md` before moving on.

---

## Stage 13 — platform confirmation and brand inputs

Asked at the start of stage 13, **before** proposing any color, font, layout, or frame size. Never
present a palette first and ask these afterwards.

### The four questions

**Question 1 is always the platform confirmation.** Pre-fill it with the stage-0 answer and label it
as such, so one click confirms. This is the last moment the platform can change cheaply — after this,
the design brief, every wireframe, and every screen are built on it.

1. **Platform — confirm before we design.** Restate the stage-0 answer *and what it commits to*, so
   the user is confirming consequences rather than a word:

   > *"Stage 0 said **mobile app (iOS + Android)**. That means: 390×844 design frame, bottom tab bar
   > with the rightmost tab as home, touch-only targets at 44px minimum, no hover states, safe-area
   > insets, and a force-update screen. Confirm, or change it?"*

   Options: *Confirm — mobile app* (pre-selected) / *Responsive web* / *Both, mobile-first* /
   *Admin back-office web*.

   **If it changes**, stop and say plainly what is now affected before continuing:
   - screens in `10-screen-list.md` that only exist on the old platform (splash and permission
     primers are mobile-only; print view and deep-link landing are web-only)
   - screens the new platform implies that are missing
   - any `NFR-13` compatibility target in `05-srs.md` that named the old platform

   Offer to revise the screen list first, then return to stage 13. Do not paper over it.

2. **Existing brand assets** — Is there a logo, brand guideline, or existing app/website whose look
   this must match? If yes, ask for the file path or URL and read it before writing the brief.
   Options: *Full brand guideline exists* / *Logo and colors only* / *Logo only* / *Nothing yet*.
3. **Locked elements** — Are any colors or fonts fixed and non-negotiable? Ask for the hex values
   and font names. Options: *Colors locked* / *Fonts locked* / *Both locked* / *Nothing locked*.
4. **Tone and theme** — Personality: formal/institutional, warm/friendly, premium/refined,
   playful, or utilitarian/efficient. And: light theme, dark theme, or both.

**Reference products** — name two or three apps or sites this should feel like, and one it should
deliberately *not* feel like — is asked in a short follow-up round, since free text is expected and
the four slots above are spent. Offer common anchors as options when the domain suggests them
(e.g. for delivery: Talabat, HungerStation, Careem).

### If the answer is "nothing exists yet"

Only then does the skill originate a direction. Propose **three** distinct directions in chat —
each one paragraph: mood, palette intent, Arabic type pairing, and *why it fits this audience* —
and let the user pick or mix before writing the full brief. Do not write three full briefs.

Make the three genuinely different (e.g. warm editorial / cool clinical precision / bold high-contrast).
Three variations of the same idea is not a choice.

### If brand assets do exist

Extract from them and state explicitly in the brief what came from the client's brand versus what
you defined to fill gaps. The client needs to know which parts they can push back on.

Record all answers in the `## Brand inputs (stage 13)` table of `00-run-log.md`. If the platform
changed, update the `Platform`, `Design frame`, `Breakpoints`, and `Navigation pattern` rows in the
`## Intake answers` table too — those are what stages 14 and 15 read.

### Then hand over the style picker — 13b

Once these four are answered you have the palette and fonts, which is everything the picker needs to
render specimens in the project's own colours. Go straight to 13b: copy
`assets/style-library.html` into the run folder, swap in the tokens, and hand it over. Do **not**
write the design brief first — §6 is written from the picks, not the other way round. See
`references/style-picker-guide.md`.
