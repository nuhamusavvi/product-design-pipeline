# Intake Questions

Stage 0 decides what can be written now. Later stages ask only when a missing fact would force
an invented business rule or would materially change a screen.

Ask with `AskQuestion` when that tool is available. If it is not available, ask in Arabic chat
and wait. Do not invent a tool name or continue as if the user had answered.

The prompt, any description the user sees, and every option label are Arabic. Ids may stay
English. Labels are short. Add **غير ذلك** when the listed options may not cover the answer.
Mark a justified suggestion with **(مقترح)** and treat it as a suggestion until the user chooses
it. Add a defer option when the decision can stay open. One batch, at most four questions. Do
not pad the batch to four.

## The rule that makes this fast

Ask only what the next meaningful decision needs. Read the source and `00-analysis-ar.md` first.

- If the answer is already there, use it. Do not ask again.
- If the gap does not block this stage, record `Q-xx` under **أسئلة مفتوحة** and continue.
- If a documented default covers it, use the default, mark it **افتراضي**, and do not ask the
  user to confirm it.
- Never invent a business rule, status, or transition. Never write an assumption as if the user
  confirmed it.
- After the user answers, update the analysis and continue from the stage that was waiting. Do
  not restart intake.
- Do not stop the run because one non-blocking question is still open.
- Do not ask for approval at the end of a stage.

**Scope defaults to MVP** unless the user specified otherwise. When the source already describes
a small initial scope, do not ask them to confirm MVP.

**A missing product name does not block analysis.** Use a temporary descriptive English slug,
mark the name **مؤقت** in the analysis, and continue.

**UI language and direction are not assumed.** Arabic requirements do not by themselves make the
interface Arabic or right to left. If a retrieved task states the interface language or
direction, record it as **مؤكد**. Otherwise record `Q-xx` and continue. Stage 8 must not tell
Lovable to use RTL unless that conclusion is supported.

**Prompts target Lovable, which builds a web UI.** Do not ask for a platform unless native-only
behavior would change a screen. Otherwise record `Q-xx` and continue with a responsive web UI.

**Brand logo, colors, and visual vibe are optional.** Do not ask for them at intake. Stage 8
uses placeholders when they are missing. Ask only if the user said a brand rule exists but did
not supply the value the prompt must obey.

---

## Stage 0 — several Plane tasks, one project

Use this when the user points at more than one Plane task, a Plane project, or pastes several
task descriptions. One pasted paragraph follows the same summary shape with a single source row.

All supplied tasks belong to the current project unless the user explicitly says some of them are
a different project. Do not open a second run per task.

### Collect

1. Make the source list first: every task the user named or pasted.
2. For each task, keep the title and the identifier when either exists. Copy the identifier
   exactly. If the identifier is missing, write **غير متوفر** and keep the title.
3. Content may arrive in two ways only:
   - The user pasted the description in the conversation.
   - A Plane tool is actually available in this session. Discover that tool's schema, then
     retrieve the named tasks. Do not invent the tool name, and do not change Plane configuration.
4. If a task was named and neither paste nor a successful retrieval produced its description,
   mark that row **لم يُقرأ**. Leave the description empty. Tell the user in Arabic which
   identifiers or titles could not be read. Do not guess the body.
5. Do not start the summary, and do not start stage 1, until every task that can be read has
   been read.

### Extract, then merge

Read each retrieved description and note its purpose before merging:

| Purpose | What to do |
|---|---|
| Requirement or workflow note | Extract the confirmed behavior into the summary |
| Bug, chore, or implementation note | Record it in the source table. Do not turn it into a product requirement unless the text states one |
| Question or empty body | Record `Q-xx` or **لم يُقرأ**. Do not fill the gap |
| Unrelated to this product | Keep the source row and exclude it from confirmed requirements. Say why |

Then merge. Overlapping statements become one confirmed requirement, with every supporting task
identifier listed. Do not drop a detail that only one task mentioned.

A conflict is two retrieved tasks that cannot both be true. Record both wordings and both
identifiers under **التعارضات**. Ask in Arabic only when choosing a side would change the next
stage. One batch, at most four questions, including any other blocking question. If the conflict
can wait, leave it and continue.

### What not to do

- Do not run stages 1–10 separately for each task.
- Do not create a screen because a Plane task exists.
- Do not treat a task title as a requirement when the description says otherwise.
- Do not analyze a task whose text was not retrieved.

### Then write section 0

Fill the summary in `references/analysis-ar.md`. It must contain the project overview, confirmed
requirements, actors and roles, functional capabilities, business workflows, conflicts, open
questions, and the source-task table. Non-critical open questions stay in that table and do not
block stage 1.

---

## Stage 0 — what to record, and what to ask

Record everything you can in the analysis header and in section 0 before asking anything.
Status is **مؤكد**, **افتراضي**, **افتراض**, or **مفتوح**.

Ask in Arabic only for gaps that block the next stage. Explain in one short Arabic line why the
answer matters when that is not obvious. Do not walk the pool below as a checklist.

### Ask from this pool only when the current stage is blocked

### Users and roles

- Which roles are in this pass, when the source names several and does not say which are in scope.
- Whether a named group is a system actor or a human role, when that changes the screens.

If the source already names the roles and what each one does, record them as **مؤكد**. Do not
ask the user to repeat them. Do not invent extra roles to fill a matrix.

### Scope depth

- MVP is the default. Ask only when the source mixes a small first release with a larger later
  product and the current section cannot say which is in scope.
- Record an explicit out-of-scope item when the user already stated one. Do not ask them to
  invent exclusions.

### Behavior that changes a screen

Ask only when two readings would produce different screens or different actions, and the source
does not settle it. Examples: whether a person can both submit and approve, or whether a stated
"update" includes a decision with named outcomes. If the screen can be specified while leaving
the unknown as `Q-xx`, do not ask.

### Platform

Ask only when a screen depends on native mobile behavior versus a responsive web layout and the
source does not say. One question, in Arabic:

> شكل الشاشة يتغير حسب هذا الاختيار. النظام يشتغل على أي منصة؟

- تطبيق ويب متجاوب (مقترح لمشروع Lovable)
- موبايل أولاً داخل المتصفح
- تطبيق موبايل أصلي (خارج Lovable)
- غير محسوم حالياً

**غير محسوم حالياً** records `Q-xx`. Continue with a responsive web prompt and state the
limitation. Do not invent a splash screen, a permission primer, or a force-update screen.

### Integrations that create screens

Payments, maps, OTP, notifications, uploads, and third-party redirects. Ask only about an
integration the current stage cannot describe without an answer. Otherwise record `Q-xx`. Do
not add the integration's screens "just in case".

### Do not ask at intake

- Product name, when a provisional slug is enough.
- Confirmation of MVP on an already-small source.
- UI language, when a retrieved task already states it. When none does, record `Q-xx`. Do not
  assume Arabic RTL.
- A design questionnaire: logo, colors, vibe, tone, light or dark, reference products.
- Scale numbers, stack, auth mechanism, database, or API shape. Those are not this pipeline's
  documents. If the source is silent, leave `Q-xx` for the backend handoff. Do not invent a
  target.

---

## Worked example — device maintenance

This example shows the policy. It is not a rule to copy into other products.

Source:

> أريد نظام لإدارة طلبات صيانة أجهزة الشركة. الموظف يرسل طلب صيانة ويحدد نوع الجهاز والمشكلة. موظف الصيانة يراجع الطلب ويحدّث حالته. المدير يستطيع مشاهدة جميع الطلبات ومتابعة حالة كل طلب.

| Item | What to do |
|------|------------|
| Product name | None was given. Provisional name: Company device maintenance. Slug: `device-maintenance`. Do not ask for a name. |
| Roles | Confirmed: employee, maintenance staff, manager. Do not ask who the users are. Do not add an administrator. |
| Behavior | Confirmed: the employee submits a request with device type and problem; maintenance staff reviews it and updates its status; the manager can see every request and each request's status. |
| Statuses | Not named. Do not invent names or transitions. Record `Q-xx` and keep writing the confirmed behavior. A review screen can say the status values are unresolved. |
| Scope | The source is a small initial workflow. Default **MVP**. Do not ask the user to confirm it. |
| Platform | Unspecified. Lovable prompts use a responsive web UI. Record `Q-xx`. Do not ask unless a later screen truly depends on a native shell. |
| Brand | Not supplied. Do not ask at intake. Stage 8 uses placeholders for logo, colors, and vibe. |
| Extra screens | Do not add sign-in, splash, force-update, notifications, or "my requests" unless the source requires them. |

No question is required to start the analysis or to draft the three screens this source supports:
submit, review-and-update-status, and all-requests. How maintenance staff reaches a request, and
which status values exist, stay open.

### Same example as three Plane tasks

This shows consolidation. It is not a retrieved Plane result.

| Task | Identifier | What the text is |
|---|---|---|
| إرسال طلب الصيانة | `MAINT-1` | Requirement: the employee submits a device type and a problem |
| مراجعة الطلب | `MAINT-2` | Requirement: maintenance staff review the request and update its status |
| زر الإرسال لا يعمل | `MAINT-3` | A bug report, not a new product requirement |

Treat `MAINT-1` and `MAINT-2` as one project. Merge them into one summary. Do not open two runs,
and do not create a screen whose only reason is that a task exists. Record `MAINT-3` in the
source table as a bug, and do not add a functional requirement from it.

If the user also names `MAINT-4` and its description is not pasted and no Plane retrieval
returns it, the source row says **لم يُقرأ**. Do not invent `MAINT-4`. Tell the user that
`MAINT-4` was not read. Continue with `MAINT-1` through `MAINT-3` when that gap is not a
blocking conflict.
