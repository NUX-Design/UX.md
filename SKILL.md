---
name: create-ux-md
description: "สร้าง UX.md จาก UX Report ทั้งหมดที่ Research มาให้กลายเป็น Context ที่ AI เข้าใจและออกแบบของตามประสบการณ์ผู้ใช้ได้ โดยสังเคราะห์หลักฐานให้เป็น Product Context, User Models, World Models, Research Synthesis และ Interaction Standards ที่นำไปใช้กับงานออกแบบและโค้ดได้จริง พร้อมระบุ provenance, gaps และสิ่งที่ยังต้อง validate"
---

# Create UX.md

Build a living UX-context source of truth that AI tools can consume directly while remaining readable by humans. Follow the UX-context design model described by Nielsen Norman Group: curate the reasoning that should steer generated product work, keep it beside the code, and continuously refine it based on what AI gets wrong. Treat complete UX Reports from research as the primary input, preserve provenance, and never disguise a suggestion as research evidence.

## UX-context design contract

`UX.md` is not a traditional handoff document and is not a replacement for `DESIGN.md`. It is curated, machine-readable context that explains who the product serves, the world those users operate in, what research has established, and how the product should behave.

Use this article-aligned output order:

1. Product context — product, value, scope, platforms, key objects, constraints, and the boundary to `DESIGN.md`.
2. User models — expertise, goals, concerns, mental models, constraints, and non-users.
3. World models — context of use, environment, frequency, devices, interruptions, stress, compliance, and error consequences.
4. Research synthesis — concise findings with evidence, source, limitations, confidence, and design implications.
5. Interaction standards — behavioral rules, applicability, exceptions, and required states.
6. Glossary — preferred domain terms, definitions, and forbidden or confusing alternatives.
7. Related artifacts — `DESIGN.md`, tokens, components, code, research, analytics, policies, and optional context indexes.
8. Context validation and maintenance — baseline versus AI output with `UX.md`, known mistakes, update triggers, and governance.

Keep provenance, assumptions, unknowns, conflicts, and readiness as supporting metadata or appendices so they do not obscure the primary context model.

For large products, `UX.md` may act as an index to additional context files or to MCP servers and agent skills. Prefer links and focused context over copying large raw research archives into the file.

## Onboard the user before synthesizing UX Reports

Start every new UX.md task with a short onboarding unless the user explicitly asks to skip it. The onboarding must use the user's language and explain:

1. What `UX.md` is: a curated, machine-readable UX Context that helps humans and AI understand the product, its users, their world, research evidence, and behavioral standards.
2. What it is for: steering AI-generated screens, flows, copy, components, and product code toward the organization's users and decisions instead of generic defaults.
3. What it is not: it is not `DESIGN.md`, not a visual token file, not a raw research archive, and not a place to invent evidence.
4. What the skill will do: inspect all available UX Reports and related artifacts first, synthesize confirmed research into AI-readable context, ask only targeted questions for high-impact gaps or conflicts, create or revise `UX.md`, validate links and coverage, and report remaining gaps.
5. What the user can provide: UX Reports, local repository paths, `PRD.md`, `DESIGN.md`, research reports or transcripts, analytics definitions, support evidence, policies, component documentation, screenshots, links, pasted notes, or answers from personal knowledge.
6. What is required versus optional: explain that a minimal start needs the UX Report or research source, the product area, the design or product decision the context should support, and where the output should live; all other inputs may be added later.
7. How to answer: the user may provide one or more Reports, correct the synthesis in free form, or say `ยังไม่ทราบ`; missing information will be labeled rather than guessed.

Use this compact onboarding shape:

```markdown
`UX.md` คือเอกสาร UX Context ที่ช่วยให้ AI และทีมเข้าใจ Product, ผู้ใช้, Context of use, Research และกติกาการทำงานของระบบ เพื่อสร้างงานที่ตรงกับผู้ใช้จริงมากกว่า UI แบบค่าเริ่มต้นทั่วไป

ผมจะช่วยตรวจ UX Report และเอกสารที่มีอยู่ → สังเคราะห์ Research ให้เป็น Context ที่ AI เข้าใจ → แยกหลักฐานออกจากสมมติฐาน → สร้างและตรวจ `UX.md`

สิ่งที่ส่งมาได้: path ของ repo, `PRD.md`, `DESIGN.md`, Research, Analytics, Component docs, Policy, ลิงก์, Screenshot, Notes หรือคำตอบจากคุณเอง
ไม่จำเป็นต้องมีครบ และตอบ `ยังไม่ทราบ` ได้

เริ่มจากส่ง UX Report และเลือกเป้าหมาย: สร้างใหม่, สังเคราะห์จากเอกสารที่มี, ตรวจไฟล์เดิม หรืออัปเดตบริบทเดิม
```

After this explanation, ask for the operating mode and repository or artifact location. If the user has already supplied a clear mode and path, acknowledge it and ask only for the first missing critical input. Do not make the user repeat information already present in accessible files.

When the user provides no artifacts, offer a guided start with the minimum inputs. When the user provides a repository, inspect `AGENTS.md`, `UX.md`, `DESIGN.md`, requirements, research, analytics, policies, and component documentation before asking questions. When the user provides a link or pasted evidence, preserve its source, date or freshness, and limitations.

## Load resources

- Read [references/interview-framework.md](references/interview-framework.md) before starting an interview, assessing completeness, or suggesting answers.
- Use [assets/UX.md.template](assets/UX.md.template) as the output structure. Adapt sections to the product, but preserve provenance, unknowns, and related-artifact references.

## Choose the operating mode after onboarding

Infer the mode from the request. Ask only if ambiguity materially changes the work.

1. **Create**: Synthesize supplied UX Reports and related artifacts into a new UX.md; ask questions only when critical context is missing.
2. **Synthesize**: Inspect all supplied research and product artifacts first, then resolve only high-impact gaps or conflicts.
3. **Audit**: Review an existing UX.md, report gaps and contradictions, then offer targeted revisions.
4. **Update**: Preserve confirmed content and change only the new or invalidated context.

For repository work, find and read applicable `AGENTS.md` first. Inspect existing `UX.md`, `DESIGN.md`, research, product requirements, analytics definitions, and component documentation before asking for information already available. Explain what was found in a short source inventory so the user knows which inputs are being used.

## Synthesize UX Reports into AI Context

Maintain an internal context ledger with four statuses:

- `confirmed`: explicitly supplied by the user or supported by a cited artifact.
- `inferred`: logically derived from confirmed context; state the reasoning and request confirmation.
- `suggested`: a plausible option or best-practice starting point, not evidence.
- `unknown`: important information that remains unavailable.

Follow this loop, using clarification questions only as a fallback:

1. Inventory every supplied UX Report and related artifact, recording source, date or freshness, scope, and limitations.
2. Extract the Report's evidence into Product Context, User Models, World Models, Research Synthesis, Interaction Standards, Glossary, and Related Artifacts.
3. Summarize the confirmed context and trace each important claim to its source.
4. Select the highest-impact unresolved topic using the priority rules in the interview framework.
5. Ask one focused clarification at a time only when the missing or conflicting information changes UX decisions, evidence quality, risk, or scope.
6. Allow free-form correction, multiple valid inputs, and “ยังไม่ทราบ”; label missing information instead of guessing.
7. Reflect the downstream implications of each clarification, detect contradictions, and preserve unresolved conflicts explicitly.
8. Skip irrelevant branches and keep the UX Report as the source of research truth.

Do not ask the user to approve every low-risk wording detail. Use reasonable defaults as `suggested`, then collect them in the final review.

## Preserve research integrity

- Never invent participants, quotes, observations, analytics, sample sizes, dates, usability results, or business constraints.
- Never convert stakeholder opinion, general best practice, or model inference into a `finding`.
- For every research insight, capture `evidence`, `source`, `confidence`, and `implication` when available.
- Write an unsupported idea as `Hypothesis`, `Assumption`, or `Suggested default`.
- Flag sensitive, regulated, accessibility-critical, destructive, financial, medical, or safety-related decisions for human validation.
- Prefer precise uncertainty over artificial completeness.

## Decide when the synthesis is complete

Generate the deliverable when:

- all supplied UX Reports have been inventoried and their relevant evidence has been mapped into the context model;
- all critical domains are confirmed or explicitly marked unknown;
- unresolved questions no longer block the stated task;
- contradictions are resolved or listed;
- the user asks to generate now; or
- further answers require research rather than conversation.

Before writing, show a compact readiness summary:

- UX Reports and source artifacts processed;
- confirmed domains;
- assumptions requiring validation;
- critical unknowns;
- recommended research actions;
- proposed output path when creating a file.

Ask for confirmation only when writing would overwrite an existing file or when a critical ambiguity would materially change the artifact.

## Produce UX.md

Use the article-aligned template and follow these rules:

- Keep content concise, actionable, and machine-readable Markdown.
- Express research as `finding → evidence → implication → interaction rule`.
- Give stable IDs to user models, world models, insights, rules, gaps, and decisions.
- Use normative language deliberately: `must`, `should`, `may`, and `must not`.
- Link to `DESIGN.md`, design tokens, components, code, research sources, analytics, policies, context files, and MCP or agent-skill sources instead of duplicating them.
- Separate confirmed facts, hypotheses, suggested defaults, and unknowns.
- Include applicability and exceptions for interaction rules.
- Put accessibility, metrics, permissions, compliance, safety, and guardrails inside the relevant product, world, research, or interaction sections unless they are important enough to require a dedicated linked artifact.
- Do not paste raw transcripts, generic personas, stock-photo descriptions, or uncurated research dumps. Preserve the underlying reasoning that changes generated design.
- Include a context-validation record: what was generated without `UX.md`, what changed with it, which rules were violated, and what should be updated next.
- Include owner, review date, and freshness metadata when known; never fabricate them.
- Preserve the product's language. If no language is specified, use the user's language and retain technical identifiers in English.

If file creation is requested, write `UX.md` beside `DESIGN.md` or at the repository root unless repo conventions require another location. Never overwrite an existing UX.md without inspecting it and obtaining action-time confirmation.

## Validate before delivery

Check:

1. Product context states the scope, value, constraints, and boundary to `DESIGN.md`.
2. User models connect expertise, goals, concerns, constraints, and non-users.
3. World models describe the real context of use and consequences of error.
4. Every critical claim has provenance or an uncertainty label.
5. Findings connect to evidence and explicit design implications.
6. Interaction rules cover loading, empty, error, success, permissions, and destructive states where relevant.
7. Terminology is consistent and forbidden synonyms are visible.
8. Accessibility, metrics, compliance, and safety requirements are testable or clearly marked proposed.
9. Links and local paths resolve when filesystem access is available.
10. Context effectiveness is evaluated against a baseline, and unknowns are prioritized by decision risk.
11. No suggested content is presented as confirmed research.

Deliver the UX.md and a short handoff containing:

- what the user supplied and which artifacts were inspected;
- completeness by domain;
- important assumptions and critical unknowns;
- what was inferred versus confirmed;
- the next recommended validation step;
- how the user can keep `UX.md` current as the product and AI output change.
