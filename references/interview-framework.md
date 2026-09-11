# UX Report synthesis framework

## Contents

0. Onboarding protocol
1. Clarification design
2. Domain map and priority
3. Smart suggestion rules
4. Evidence model
5. Completeness rubric
6. Guidance for missing information

## 0. Onboarding protocol

Before asking for UX details, orient the user in plain language. Use the user's language; when the user writes Thai, use Thai.

Explain these points briefly:

- `UX.md` is a machine-readable UX Context for humans and AI.
- It captures Product Context, User Models, World Models, Research Synthesis, Interaction Standards, Glossary, Related Artifacts, and Context Validation.
- It helps AI-generated design and code reflect real users, domain language, research, and behavioral rules.
- It is not `DESIGN.md`, a raw transcript archive, or permission to invent evidence.
- The user can provide repository paths, existing Markdown, research, analytics, policies, screenshots, links, pasted notes, or personal knowledge.
- A minimum viable start is a UX Report or research source, product area, decision to support, and output location. Everything else can be unknown or added later.
- The user may provide one or more Reports, correct the synthesis freely, or say `ยังไม่ทราบ`.

Use a short orientation before the first question:

```markdown
`UX.md` คือเอกสาร UX Context ที่ช่วยให้ AI และทีมเข้าใจ Product, ผู้ใช้, Context of use, Research และกติกาการทำงานของระบบ เพื่อสร้างงานที่ตรงกับผู้ใช้จริงมากกว่า UI แบบค่าเริ่มต้นทั่วไป

ผมจะตรวจ UX Report และข้อมูลที่มีอยู่ → สังเคราะห์ Research ให้เป็น Context ที่ AI เข้าใจ → แยกหลักฐานออกจากสมมติฐาน → สร้างและตรวจ `UX.md`

คุณส่ง path ของ repo, `PRD.md`, `DESIGN.md`, Research, Analytics, Policy, Component docs, ลิงก์, Screenshot, Notes หรือคำตอบจากคุณเองได้ และไม่จำเป็นต้องมีครบ
```

Then ask the user to choose or correct the mode:

- **Create** — synthesize supplied UX Reports into a new UX Context.
- **Synthesize** — inspect supplied artifacts and fill only high-impact gaps or conflicts.
- **Audit** — review an existing `UX.md` for gaps and contradictions.
- **Update** — preserve confirmed context and change only new or invalidated information.

Also request the repository or artifact location when it is not already known. If the user supplied a clear mode and path, do not ask them to repeat it.

Provide this preparation checklist when useful:

| Input | Required to start? | How it helps |
|---|---:|---|
| Product area and decision | Yes | Sets scope and prevents irrelevant context |
| Primary user and goal | Yes | Determines user and world-model questions |
| Output path or repository | Yes when writing a file | Determines where the source of truth belongs |
| `PRD.md` or requirements | Helpful | Clarifies product scope and constraints |
| `DESIGN.md`, tokens, and components | Helpful | Keeps visual rules in the correct source |
| Research, interviews, support evidence | Helpful | Supports findings and confidence |
| Analytics and dashboards | Optional | Supports behavior and outcome validation |
| Policies, accessibility, privacy, or compliance | Conditional | Adds safeguards for sensitive decisions |
| Screenshots, links, or notes | Optional | Adds examples and provenance when available |

Never make completeness a prerequisite for starting. Convert missing inputs into explicit `unknown`, `hypothesis`, or `suggested default` entries and explain the smallest validation action that can reduce the uncertainty.

## 1. Clarification design

Ask for clarification in plain language and keep each turn easy to answer. Do not interview for information already present in a UX Report.

Use this response shape when choices help:

```markdown
จาก UX Report และข้อมูลก่อนหน้า [brief context], เรื่องที่ยังมีผลต่อ [decision] คือ [topic].

คำถามเพื่อยืนยันหรือแก้ความขัดแย้ง: ...?

- A — ... ผลต่อ UX: ...
- B — ... ผลต่อ UX: ...
- C — ... ผลต่อ UX: ...
- ยังไม่ทราบ — ผมจะช่วยวางวิธีหาคำตอบให้

เลือกได้มากกว่าหนึ่งข้อเมื่อเกี่ยวข้อง หรือพิมพ์คำตอบของคุณเองได้
```

Do not offer cosmetic choices that do not affect a decision. Do not use overlapping options unless explicitly allowing multiple selections. Treat the UX Report as the primary research source and ask only about material gaps or conflicts.

After an answer, reflect it using:

```text
Captured: [answer] (confirmed)
Implication: [what this changes]
Still uncertain: [only if material]
```

## 2. Domain map and priority

Prioritize questions by `decision impact × uncertainty × risk`. Cover only relevant domains.

| Priority | Domain | Minimum useful context |
|---|---|---|
| Critical | Product context | product/value, scope, lifecycle, platforms, key objects, constraints, `DESIGN.md` boundary |
| Critical | User models | primary users, expertise, goals, concerns, mental models, constraints, non-users |
| Critical | World models | frequency, session length, environment, devices, interruptions, stress, compliance, error consequences |
| Critical | Research synthesis | findings, evidence, source/freshness, confidence, limitations, design implications |
| High | Interaction standards | navigation, information density, forms, feedback, errors, permissions, destructive actions, recovery |
| High | Glossary | preferred terms, definitions, forbidden alternatives, localization or reading-level needs |
| High | Related artifacts | `DESIGN.md`, tokens, components, code, research, analytics, policies, context indexes |
| Medium | Context validation | baseline without `UX.md`, observed AI mistakes, output changes, next validation action |
| Medium | Governance | owner, reviewers, review cadence, update triggers, freshness risks |

First map product scope, primary user model, context of use, and evidence from the supplied UX Reports. Ask about missions, accessibility, metrics, compliance, or guardrails only when the Report is silent or conflicting and the answer changes the context or a decision.

The output should follow this order: product context → user models → world models → research synthesis → interaction standards → glossary → related artifacts → context validation and maintenance. Supporting provenance, assumptions, unknowns, conflicts, and readiness may appear as metadata or appendices.

## 3. Smart suggestion rules

Derive options from confirmed context and state the connection.

- Frequent expert use → suggest higher information density, shortcuts, bulk actions, persistent filters, and fewer tutorials; record this as a world-model implication, not a generic UI preference.
- Infrequent novice use → suggest progressive disclosure, recognizable language, guided steps, safe defaults, and resumability.
- High consequence of error → suggest prevention, review, explicit confirmation, audit trail, permissions, and recovery.
- Reversible low-risk action → suggest immediate action with undo rather than repeated confirmation.
- Mobile or interrupted environment → suggest short steps, autosave, resumability, large targets, and offline/error recovery.
- Weak network → suggest optimistic behavior only when safe, explicit sync states, retry, cached essentials, and partial failure handling.
- Multiple roles → suggest role-based missions and permissions; avoid assuming one shared journey.
- Regulated or sensitive data → suggest least privilege, consent, retention rules, redaction, auditability, and policy review.
- International audience → suggest localization, variable-length copy, locale-aware formats, and avoidance of culture-specific assumptions.
- No research evidence → offer hypotheses and a lean validation plan, never findings; mark the context as provisional.

For each suggested option, explain both its rationale and tradeoff. Avoid recommending a pattern merely because it is common.

## 4. Evidence model

Use these evidence levels:

| Level | Meaning | Allowed language |
|---|---|---|
| E3 | Direct, relevant, sufficiently recent evidence with traceable source | `Finding`, with limitations |
| E2 | Relevant but limited, indirect, old, or small-coverage evidence | `Indicative finding`, with caution |
| E1 | Stakeholder report, support anecdote, benchmark, or unverified artifact | `Signal` or `Assumption` |
| E0 | No evidence | `Hypothesis` or `Suggested default` |

Do not infer E3 from the mere existence of a report. Ask what supports the claim. Record conflicts between sources instead of averaging them away.

Recommended insight record:

```yaml
- id: INS-001
  status: confirmed | inferred | suggested | unknown
  evidence_level: E0 | E1 | E2 | E3
  statement: "..."
  source: "..."
  limitations: "..."
  implication: "..."
  ux_rule_refs: [RULE-001]
```

Recommended context records:

```yaml
- id: USER-001
  status: confirmed | inferred | suggested | unknown
  role: "..."
  expertise: "..."
  goals: ["..."]
  concerns: ["..."]
  constraints: ["..."]
  source: "..."

- id: WORLD-001
  status: confirmed | inferred | suggested | unknown
  environment: "..."
  interruptions: "..."
  error_consequences: "..."
  design_implications: ["..."]
  source: "..."
```

## 5. Completeness rubric

Score each applicable domain:

- `2 Ready`: enough confirmed context to guide a decision.
- `1 Provisional`: usable with explicit assumptions or limited evidence.
- `0 Missing`: unknown and decision-blocking.
- `N/A`: genuinely irrelevant; include rationale.

Do not hide critical zeros inside a total percentage. Report domain scores and blockers. A UX.md can be ready for an early prototype while not ready for production decisions.

Readiness labels:

- `Discovery`: scope and hypotheses captured; research gaps remain.
- `Prototype-ready`: enough context for bounded design exploration.
- `Delivery-ready`: behavior, content, accessibility, and edge cases are testable.
- `Production-governed`: evidence, metrics, ownership, and update process are operational.

## 6. Guidance for missing information

When the user selects “ยังไม่ทราบ”, respond with four parts:

1. **Why it matters**: name the decision affected.
2. **Fastest reliable source**: point to analytics, interviews, support logs, domain experts, usability tests, policies, or code as appropriate.
3. **Suggested temporary answer**: provide 2–3 contextual options labeled `suggested`, including risk.
4. **Validation action**: give a small concrete task, owner type, and success signal.

Examples:

- Unknown primary segment: inspect recent active accounts and conduct 3–5 exploratory interviews across distinct roles; do not fabricate a persona.
- Unknown error cost: map failure scenarios with product, support, security, or operations; use conservative safeguards until validated.
- Unknown accessibility target: suggest WCAG 2.2 AA as a provisional web baseline, then confirm legal, market, and organizational requirements.
- Unknown success metric: define the user outcome first, then select one behavioral measure and one harm/quality guardrail; mark both as proposed until instrumentation is verified.
- Conflicting stakeholder answers: record the conflict, identify the decision owner, and seek behavioral or research evidence rather than choosing by seniority alone.
