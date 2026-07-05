# POV Judgment (Hard Rules)

Signals from [scan-signals.md](./scan-signals.md) get classified here. **Context is mandatory** — a signal word in isolation is not a finding.

## POV leakage failure types

| Type | Description | Typical severity |
|---|---|---|
| **Policy negation** | "We don't / 하지 않습니다" stating internal limits instead of user benefit | P0–P1 |
| **System agency** | System or AI as subject making choices user didn't ask about | P0–P1 |
| **Mode jargon** | Internal mode names (A/B), restriction rationale, no situational user choice | P0–P1 |
| **Planning / meta** | Design intent, PRD language, "설계상", "기획상" | P1 |
| **Prompt residue** | Instruction tone, role preamble, chain-of-thought visibility | P0 |
| **False-trust** | Trust copy that explains mechanism instead of control/predictability/outcome | P0–P1 |

A single string can hit multiple types. Classify by **worst** type present.

## UI vs README audience

| Surface | Reader | Passes | Fails |
|---|---|---|---|
| UI / widget / onboarding | End user of the product | "Pick an idea → get a brief" | "Mode A limits depth per PRD" |
| README quick start | Developer onboarding the repo | "Clone → `pnpm dev` → edit `src/foo`" | "Our philosophy is shallow-first ideation" |
| README architecture (narrow) | Developer finding code | Folder map, module roles, data flow | Why modes exist, AI selection criteria |
| Docs / FAQ | User or integrator | "Export gives you a Markdown brief" | "We separated must-have vs nice-to-have per sprint policy" |
| Errors | User blocked on a task | "Add a title to continue" | "Validation failed: schema constraint" |

## README narrow architecture pass (hard rule)

When a README or doc section is labeled Architecture, Structure, or How it works:

### PASS — keep as-is

- Directory / folder structure
- Module locations and responsibilities
- Data flow needed to onboard (request → handler → store)
- Run, deploy, env vars, edit points
- Where to change X if you want to customize Y

### NOT PASS — P0/P1 even if labeled architecture

- Product philosophy or positioning
- Mode restriction rationale ("B mode exists because…")
- AI judgment criteria (scoring, selection logic, prompt strategy)
- PRD design intent ("we chose shallow depth to…")
- Feature tiering policy ("must-have vs later" as team process, not user outcome)

**Test:** Would this paragraph help someone **find and change code**? If it only helps someone **understand why the PM designed it** → leakage.

## Trust sentence rule (hard rule)

Trust copy must pass the **control / predictability / outcome** test.

| Pass | P0/P1 |
|---|---|
| User control — what they can set, skip, export, delete | System/AI internal mechanism |
| Predictability — what happens, in what order, what won't repeat | Model parameters, pipeline stages, chunking |
| Outcome — what they receive, when, in what format | Policy negation as trust ("we don't store…") without user framing |

**Example (Korean):**

- Bad: `AI가 다음 질문을 고릅니다` — system agency, false-trust
- Good: `답변에 맞춰 필요한 질문만 이어집니다` — predictability + user benefit

## P0 / P1 / P2 / Pass

| Class | Criteria | Phase 2 action |
|---|---|---|
| **P0** | User-facing; exposes system/AI agency, prompt residue, or false-trust in primary flow (hero, onboarding, core widget) | Must fix |
| **P1** | User-facing; policy negation, mode jargon, planning/meta, README philosophy-as-architecture | Must fix |
| **P2** | Minor tone leakage; understandable but not optimal; edge-case surfaces | Fix if time; may defer |
| **Pass** | User POV; action/benefit/outcome/control | No change |

**Escalation:** P2 in a trust section or hero → treat as P1.

**De-escalation:** Never below P2 if policy negation is the main clause.

## Fixture examples (test only — not rules)

BriefOn / Interview SaaS before/after strings live in [rewrite-formula.md § Korean fixtures](./rewrite-formula.md) and [§ English fixtures](./rewrite-formula.md) — **SSOT for copy fixtures**.

Use fixtures to calibrate **classification**, not as a product patch list:

| Fixture string (see rewrite-formula) | Leakage type | Typical class |
|---|---|---|
| A모드에서 너무 깊게 들어가지 않습니다 | Policy negation + mode jargon | P1 |
| AI가 다음 질문을 고릅니다 | System agency + false-trust | P0 |
| 브리프가 최종 목적입니다 | Planning / meta | P1 |

Apply the same lens to any product's strings.