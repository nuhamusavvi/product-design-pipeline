# Arabic Analysis — Stages 0 through 7

Write one file: `product-design/NN-slug/00-analysis-ar.md`. Add the section for the current
stage. Do not rewrite earlier sections unless a later answer changes a fact, and then edit in
place. Do not create a second file for these stages.

The file is Arabic. Permanent IDs, and a real technical name the source already used, stay as
they are. Status words in tables: **مؤكد**, **افتراضي**, **افتراض**, **مفتوح**.

Load this file at stage 0 for the skeleton, then again only if the current stage's section is
not already in context. Do not load legacy templates.

## Skeleton

Create this skeleton at stage 0 and fill section 0. Leave later headings out until that stage
starts, so an unfinished run shows exactly how far it got.

```markdown
# تحليل المنتج — <الاسم>

- المجلد: product-design/NN-slug/
- اسم المنتج: مؤكد | مؤقت — <الاسم>
- النطاق: MVP (افتراضي) | كما حدده المستخدم
- لغة الواجهة: كما ذكرها المصدر | غير محددة (Q-xx). لا تفترض الاتجاه من لغة المتطلبات.
- تاريخ البدء: <date>

## تقدم المراحل

- [ ] 0. فهم المتطلبات
- [ ] 1. النطاق والمتطلبات الوظيفية
- [ ] 2. الأدوار والصلاحيات
- [ ] 3. سير العمل
- [ ] 4. جرد الشاشات
- [ ] 5. حالات الواجهة والتحقق
- [ ] 6. تدفقات المستخدم والتنقل
- [ ] 7. مواصفات الواجهة
- [ ] 8. مطالبة نظام التصميم
- [ ] 9. مطالبات الشاشات
- [ ] 10. تسليم الخلفية

## مصادر المهام

املأ هذا الجدول قبل الملخص. صف واحد لكل مهمة مذكورة، بما فيها التي لم تُقرأ.

| معرف المهمة | العنوان | الغرض | القراءة | ماذا أُخذ منها |
|---|---|---|---|---|
| <كما هو، أو غير متوفر> | | متطلب \| سير عمل \| خلل \| سؤال \| غير متعلق | قُرئت \| لم يُقرأ | معرفات الملخص، أو سبب الاستبعاد |

لا تكتب وصفاً في عمود «ماذا أُخذ منها» لمهمة حالتها **لم يُقرأ**.

## النصوص المقروءة

انسخ نص كل مهمة قُرئت فقط، تحت عنوانها ومعرفها. لا تنسخ مهمة لم يصل نصها.

## المصطلحات

| المصطلح في المصدر | المصطلح في تسليم الخلفية | الحالة |
|---|---|---|
| | | |

## 0. ملخص المتطلبات

### نظرة عامة على المشروع

<فقرة قصيرة من المهام المقروءة. المؤكد فقط. إذا لم تُقرأ بعض المهام، اذكر معرفاتها هنا ولا تكمّل قصتها.>

### المتطلبات المؤكدة

| البيان | مهام المصدر | الحالة |
|---|---|---|
| | MAINT-1، MAINT-2 | مؤكد |

ادمج التكرار. أبقِ كل تفصيل لا يشترك فيه إلا مصدر واحد، واذكر مهمة ذلك المصدر.

### الأدوار

| الدور | الأفعال التي ذكرتها المهام | مهام المصدر | ما لم يُذكر |
|---|---|---|---|
| | | | |

### القدرات الوظيفية

| القدرة | مهام المصدر | الحالة |
|---|---|---|
| | | مؤكد |

هذه قائمة المرحلة 0. المرحلة 1 تعطيها `FR-xx` ولا تعيد قراءة Plane.

### سير العمل

اكتب الخطوات التي تدعمها المهام المقروءة. المرحلة 3 تعطيها `W-xx`.

1. 
2. 

### التعارضات

| الموضوع | الصيغة الأولى | مهمتها | الصيغة الثانية | مهمتها | القرار |
|---|---|---|---|---|---|
| | | | | | مفتوح \| سُئل المستخدم |

إذا لا يوجد تعارض، اكتب: لا يوجد.

### أسئلة مفتوحة

| المعرف | السؤال | ماذا يمنع | ماذا يمكن إكماله بدونه |
|---|---|---|---|
| Q-01 | | | |

سؤال غير حاجز لا يوقف المرحلة 1.

### افتراضات

| المعرف | الافتراض | لماذا أُضيف | أثره |
|---|---|---|---|
| A-01 | | | |

### قيود ذكرها المصدر

- 
```

Tick stage 0 in **تقدم المراحل** when section 0 is written. Tick each later stage the same way.
Do not ask the user to approve the tick.

## Stage 1 — النطاق والمتطلبات الوظيفية

Append:

```markdown
## 1. النطاق والمتطلبات الوظيفية

لا تعد كتابة القسم 0. أضف ما يلي فقط، وأحل إلى معرفات المهام الموجودة.

### الغرض والمستخدمون والهدف

- **الغرض:** 
- **المستخدمون:** 
- **الهدف التجاري المذكور:** <أو Q-xx إذا لم يُذكر>

### داخل النطاق

- 

### خارج النطاق

<فقط ما استبعده المصدر، أو ما يبقى خارج MVP لأن المصدر لم يطلبه. لا تحذف مطلباً مذكوراً بحجة MVP.>

### المتطلبات الوظيفية

| المعرف | المتطلب | مهام المصدر | الحالة |
|---|---|---|---|
| FR-01 | | معرف المهمة من القسم 0 | مؤكد \| تفسير غير مؤكد |

التفسير غير المؤكد ليس مطلباً مؤكداً. لا تعطِه `FR-xx` إلا إذا بقي موسوماً بأنه غير مؤكد.

### قواعد العمل المذكورة

| المعرف | القاعدة | مهام المصدر | الحالة |
|---|---|---|---|
| BR-01 | | | مؤكد |

### القيود والاعتمادات

- **قيد:** <أو لا يوجد>
- **اعتماد:** <نظام ذكره المصدر، أو لا يوجد>

### تعارضات ما زالت مفتوحة

<أحل إلى جدول التعارضات في القسم 0، أو اكتب: لا يوجد.>
```

An `FR-xx` restates a capability already extracted in section 0. Copy the Plane task identifiers
into **مهام المصدر**. Do not retrieve Plane again. An `BR-xx` is a rule the retrieved text states
("must", "only", "cannot", a named limit). If the sentence does not state a rule, do not write
`BR-xx`. Put the gap in `Q-xx`.

Do not add conventional features (accounts, notifications, dashboards, reports, audit logs) as
functional requirements. If one seems necessary to reach a confirmed screen, record `A-xx` or
`Q-xx` and do not treat it as confirmed.

## Stage 2 — الأدوار والصلاحيات

Append:

```markdown
## 2. الأدوار والصلاحيات

| المعرف | الدور | الغرض | ما يصل إليه | الأفعال | الممنوع إذا ذُكر | الفرق عن دور آخر | مهام المصدر | غير المحسوم |
|---|---|---|---|---|---|---|---|---|
| P-01 | | | | | | | من القسم 0 | Q-xx |
```

One row per actor the retrieved text supports. Leave restricted actions empty when the source
does not forbid them. Do not invent a permission matrix.

## Stage 3 — سير العمل

Append one block per confirmed process:

```markdown
## 3. سير العمل

### W-01 — <اسم قصير>

- **المحفز:** 
- **الفاعل:** P-0x
- **الشروط السابقة:** 
- **المتطلبات والقواعد:** FR-xx، BR-xx
- **مهام المصدر:** 
- **الشاشات:** تُملأ بعد المرحلة 4
- **الحالة:** مؤكد | فيه نقاط مفتوحة

1. 
2. **قرار:** <فقط إذا ذكره المصدر، وإلا لا ترسم فرعاً>
3. **النتيجة:** 

**الاستثناء أو الفشل:** <أو Q-xx>
**ما لم يُحسم:** Q-xx
```

Keep only workflows that change the screens or the handoff. A short mermaid diagram is allowed
when the source has a real branch. Do not label a node with an invented status. Do not produce HTML.

## Stage 4 — جرد الشاشات

Append:

```markdown
## 4. جرد الشاشات

| المعرف | الاسم بالعربي | الاسم الإنجليزي للملف | النوع | الفاعل | الغرض | ما يُعرض | الأفعال | الدخول | الخروج | سير العمل | الصلاحية | الاعتماد | أسئلة |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| SC-01 | | submit-request | صفحة \| حوار \| درج \| تبويب \| سطح آخر | P-0x | | | | | | W-0x | | | |
```

This table is the source for stage 9. Rules:

- Every row comes from a confirmed actor action or workflow step.
- Combine screens that are the same task. Keep them separate when the actor, actions, or
  permission differ. Say which choice you made.
- Before leaving the stage, note missing steps, duplicate rows, and rows that should be merged.
- Do not add a screen because other products have it.
- `النوع` is صفحة, حوار, درج, تبويب, or another surface the requirements support.
- IDs start at `SC-01` and are never renumbered.
- Mark **محجوبة** only when a prompt cannot be written without inventing a rule. Name the `Q-xx`.

## Stage 5 — حالات الواجهة والتحقق

Append one block per `SC-xx`. Include a state only when that screen can actually reach it.
Candidates are: initial, loading, empty, success, error, disabled, validation, permission,
confirmation, destructive confirmation, conditional fields, status-dependent controls, search,
filter, pagination, submit, and retry. Skip the rest. Do not write a test document.

```markdown
## 5. حالات الواجهة والتحقق

### SC-01 — <اسم الشاشة>

| الحالة | متى تظهر | ماذا يرى المستخدم | البيانات اللازمة | التوثيق |
|---|---|---|---|---|
| | | | | مؤكد \| مفتوح |

**التحقق:** <فقط قاعدة ذكرها المصدر. الناقص الحاجز يصبح Q-xx.>
**الإرسال أو إعادة المحاولة:** 
```

Validation describes the user-facing rule ("لا يُرسل الطلب بدون نوع الجهاز") only when the
source requires that field. Do not invent length limits, formats, or error codes.

## Stage 6 — تدفقات المستخدم والتنقل

Append:

```markdown
## 6. تدفقات المستخدم والتنقل

### F-01 — <اسم التدفق>

- **الفاعل:** P-0x
- **يحقق:** W-0x
- **البداية:** SC-0x
- **النهاية:** SC-0y
- **الحالة:** مؤكد \| فيه أسئلة مفتوحة

1. SC-0x — <الفعل>
2. قرار، فقط إذا ذكره المصدر
3. SC-0y — 

**الإلغاء أو الفشل:** 
**التنقل العام:** <فقط عناصر ذكرها المصدر>
**نقص في الجرد:** 
```

If a workflow step has no screen, add the screen to section 4 or record why it is blocked, then
update this flow. Do not leave the gap for stage 9. Do not invent a navigation item. The `F-xx`
order is the prompt order.

## Stage 7 — مواصفات الواجهة

Append one block per non-blocked screen. This is the source stage 9 copies from. Do not restate
the whole analysis; point at IDs and write the screen-level detail.

```markdown
## 7. مواصفات الواجهة

### مكوّنات مشتركة

| الاسم | أين يُستخدم | ماذا يعرض | أسئلة |
|---|---|---|---|
| | SC-01، SC-02 | | |

### هوية الواجهة للمطالبات

- **المنتج والجمهور:** 
- **لغة الواجهة واتجاهها:** مؤكد | Q-xx. لا تفترض RTL.
- **الاستجابة:** 
- **الشعار والألوان والمزاج البصري:** ما زوّده المستخدم فقط، وإلا غير مزوّد
- **قيود تصميم مذكورة:** 
- **أسئلة تؤثر على الواجهة:** Q-xx

### SC-01 — <اسم الشاشة>

- **الغرض والفاعل والصلاحية:** 
- **التدفق:** F-0x
- **الترتيب والمكوّنات:** 
- **الحقول والتحقق:** 
- **الحالات:** من القسم 5
- **الدخول والخروج:** 
- **نصوص الواجهة المطلوبة:** <بلغة الواجهة المؤكدة، أو اتركها مفتوحة>
- **قواعد عمل تظهر في الشاشة:** BR-xx
- **لا تُضف:** 
- **ما لا يجوز اختراعه:** Q-xx
```

Cover every `SC-xx` that is not **محجوبة**. For a blocked screen, name the missing decision and
do not invent the specification. Do not draw a wireframe or write HTML.

Tick stages 8–10 in the progress list only when those files exist. Do not create them here.
