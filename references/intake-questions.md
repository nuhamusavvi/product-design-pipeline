# Intake Questions

Stage 0 decides what can be written now. Stage 13 settles whatever visual design still needs.
Ask with `AskQuestion` when that tool is available. If `AskQuestion` is not available, ask in
Arabic chat and wait. Do not invent a tool name or continue as if the user had answered.

The prompt, any description the user sees, and every option label are Arabic. Ids may stay
English. Labels are short. Add **غير ذلك** when the listed options may not cover the answer.
Mark a justified suggestion with **(مقترح)** and treat it as a suggestion until the user chooses
it. Add a defer option when the decision can stay open. One batch, at most four questions. Do
not pad the batch to four.

## The rule that makes this fast

Ask only what the next meaningful decision needs. Read the source and `00-run-log.md` first.

- If the answer is already there, use it. Do not ask again.
- If the gap does not block this stage, record `Q-xx` under **Open Questions** in `01-prd.md` §8
  and continue.
- If a documented default covers it, use the default, mark it **Default**, and do not ask the
  user to confirm it.
- Never invent a business rule, status, or transition. Never write an assumption as if the user
  confirmed it.
- After the user answers, update the run log and continue from the stage that was waiting. Do
  not restart intake.

**Scope defaults to MVP** unless the user specified otherwise. When the source already describes
a small initial scope, do not ask them to confirm MVP.

**A missing product name does not block analysis.** Use a temporary descriptive English name,
mark it **Provisional** in the run log, and continue.

---

## Stage 0 — what to record, and what to ask

Record everything you can in the `## Intake answers` table before asking anything. Status is
**Confirmed**, **Default**, **Assumption**, or **Open**.

Ask in Arabic only for gaps that block the next stage. Explain in one short Arabic line why the
answer matters when that is not obvious. Do not walk the pool below as a checklist.

### Platform

Ask only when the platform is unspecified **and** the current decision needs it (screen list,
navigation, frame, or any other choice the platform would change). Do not assume one.

Options:

- تطبيق موبايل
- تطبيق ويب
- الاثنين معاً
- غير محسوم حالياً

If the user chooses **غير محسوم حالياً**, record the open question and continue with any work
that does not depend on a frame. Do not invent a platform. Before wireframes or UI screens, this
question blocks.

When they choose, map the answer onto one profile in `design-brief-template.md` §Platform
profiles and record the frame, breakpoints, and navigation pattern. A web product that is
clearly an internal admin tool uses the admin profile; note that in the run log. Do not add a
fifth option unless that split itself blocks the current decision.

Follow-ups, only when that answer makes them blocking:

- **تطبيق موبايل**: iOS, Android, or both — only if the design would actually differ.
- **تطبيق ويب or الاثنين معاً**: a minimum width or print support — only if a screen depends on it.
- A separate admin panel — only if the source leaves it unclear whether this run includes it.

Do not ask the platform question again after it has been answered.

### Ask from this pool only when the current stage is blocked

### Users and roles

- Which roles are in this pass, when the source names several and does not say which are in scope.
- Whether a role is only a back-office user, when that would put its screens in another run.
- Digital literacy of the primary user, when density and guidance cannot be chosen without it.

If the source already names the roles and what each one does, record them as **Confirmed**. Do
not ask the user to repeat them.

### Scope depth

- MVP is the default. Ask only when the source mixes a small first release with a larger later
  product and the current document cannot say which is in scope.
- Record an explicit out-of-scope item when the user already stated one. Do not ask them to
  invent exclusions.

### Locale and content

- Primary market, when currency, address, phone format, or calendar is otherwise unknown and the
  current stage needs it.
- UI language stays **Arabic only, RTL** unless the user said otherwise. That is a default. Do
  not ask them to confirm it.
- Digits are always Latin `0-9`. Do not ask.
- Calendar: Gregorian, Hijri, or both — only when a screen or a rule depends on it.

### Integrations that create screens

Payments, maps, OTP, notifications, uploads, chat, and third-party redirects. Ask only about an
integration the current stage cannot describe without an answer. Otherwise record `Q-xx`.

### Constraints

Existing backend, deadline, regulation, and accessibility. WCAG 2.1 AA is the default
accessibility assumption; mark it **Assumption** and do not ask the user to confirm it unless a
different target is already in play.

### Engineering inputs — stages 5 to 7

Do not spend stage-0 questions on these. When the source is silent, propose a documented
assumption or leave `Q-xx`. Ask only when the SRS, data model, or API cannot be written without
the answer.

- Scale numbers, when an `NFR-xx` would otherwise have no target. A missing number becomes an
  open question, not an invented target.
- Availability, stack preference, auth model, residency, and who receives the handoff — ask at
  the stage that needs them, or record them as open.

### Worked example — device maintenance

This example shows the policy. It is not a rule to copy into other products.

Source:

> أريد نظام لإدارة طلبات صيانة أجهزة الشركة. الموظف يرسل طلب صيانة ويحدد نوع الجهاز والمشكلة. موظف الصيانة يراجع الطلب ويحدّث حالته. المدير يستطيع مشاهدة جميع الطلبات ومتابعة حالة كل طلب.

| Item | What to do |
|------|------------|
| Product name | None was given. Provisional name: Company device maintenance. Slug: `device-maintenance`. Do not ask for a name. |
| Roles | Confirmed: employee, maintenance staff, manager. Do not ask who the users are. |
| Behavior | Confirmed: the employee submits a request with device type and problem; maintenance staff reviews it and updates its status; the manager can see every request and each request's status. |
| Statuses | Not named. Do not invent names or transitions. Record `Q-xx` in the PRD and keep writing the confirmed behavior. Ask later only if the next decision needs the names. |
| Scope | The source is a small initial workflow. Default **MVP**. Do not ask the user to confirm it. |
| Platform | Unspecified. It does not block the PRD. Record `Q-xx`. When the screen list or the design brief needs it, ask in Arabic: تطبيق موبايل / تطبيق ويب / الاثنين معاً / غير محسوم حالياً. One short line on why: شكل الشاشات والتنقل يتغير حسب هذا الاختيار. |

No other question is required to start the PRD.

---

## Stage 13 — platform, if still open, and brand inputs

Asked at the start of stage 13, **before** any color, font, layout, or frame size. Never present
a palette first.

### Platform

If `00-run-log.md` already has a confirmed platform, use it. Do not ask again. Write the frame,
breakpoints, navigation pattern, and input model into `13-design-brief.md` §0.

If it is still **Open**, this question blocks visual design. Ask it in Arabic and wait:

> شكل الشاشات والتنقل يتغير حسب هذا الاختيار. النظام يكون على أي منصة؟

- تطبيق موبايل
- تطبيق ويب
- الاثنين معاً
- غير محسوم حالياً

**غير محسوم حالياً** means stop before wireframes and UI screens. Do not pick a profile yourself.

If the user changes a platform that earlier documents already used, stop and say what is affected
before continuing:

- screens in `10-screen-list.md` that exist only on the old platform (splash and permission
  primers are mobile-only; print view and a deep-link landing are web-only)
- screens the new platform implies that are missing
- any `NFR-13` compatibility target in `05-srs.md` that named the old platform

Offer, in Arabic, to revise the screen list first, then return to stage 13.

### Brand questions

Ask only the ones still unanswered. Skip any the user already answered. At most four questions
in the batch, including the platform question when it is still open.

1. **Existing brand** — a logo, a brand guide, or an existing app or site this must match.
   Options: يوجد دليل هوية كامل / شعار وألوان فقط / شعار فقط / ماكو شي حالياً.
   If something exists, ask for the file path or URL and read it before writing the brief.
2. **Locked elements** — colors or fonts that cannot change. Options: الألوان ثابتة / الخطوط
   ثابتة / الاثنين ثابتة / ماكو شي ثابت. Ask for hex values and font names only after they say
   something is locked.
3. **Tone and theme** — formal, warm, premium, playful, or utilitarian, and light, dark, or both.
   Offer those as short Arabic labels. Include غير ذلك.

**Reference products** — two or three products this should feel like, and one it should not —
go in a later round, because the answer is free text. Offer familiar anchors when the domain
suggests them. Skip this round when the user already named references or when brand assets
already fix the direction.

### If the answer is "ماكو شي حالياً"

Only then does the skill originate a direction. Propose **three** distinct directions in Arabic
— each one short paragraph: mood, palette intent, Arabic type pairing, and why it fits this
audience — and let the user pick or mix before writing the full brief. Do not write three full
briefs. The three directions must be genuinely different. The written brief itself stays English.

### If brand assets do exist

Extract from them and state in the brief what came from the client's brand versus what you
defined to fill gaps.

Record the answers in `## Brand inputs (stage 13)` of `00-run-log.md`. If the platform was
answered or changed here, update the platform, frame, breakpoints, and navigation rows in
`## Intake answers` too.

### Then hand over the style picker — 13b

Once the platform is settled and the palette and fonts are known, go to 13b: copy
`../assets/style-library.html` into the run folder, swap in the tokens, and hand it over. Do
**not** write the design brief first — §6 is written from the picks, not the other way round.
See `style-picker-guide.md`.
