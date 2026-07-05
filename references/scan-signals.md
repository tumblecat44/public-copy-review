# Scan Signals

**Explicit:** Signals are NOT final judgment. Every hit requires context judgment in [pov-judgment.md](./pov-judgment.md).

Use signals to **accelerate search**, not to auto-flag. Example keywords are **search accelerators only** — NOT a banned word list. A clean grep with zero hits does not mean the audit is done.

## Required scan behavior

1. Run grep/search per category below in scoped files.
2. **Read all visible strings** in scoped surfaces even when grep returns nothing.
3. For each candidate, classify in pov-judgment — do not report a finding on keyword alone.

## Signal categories

### 1. Policy negation

Team stating what they refuse to do instead of what the user gets.

**Accelerators (KO):** `하지 않습니다`, `하지 않아요`, `안 합니다`, `제한`, `들어가지 않`, `깊게 하지`, `고정`

**Accelerators (EN):** `don't`, `do not`, `won't`, `we never`, `restricted`, `not designed to`, `avoid`, `prevent`

**Often leakage when:** Main clause is the negation; benefit is absent or subordinate.

### 2. System agency

System, AI, model, or "we" as subject performing opaque choices.

**Accelerators (KO):** `AI가`, `시스템이`, `자동으로 선택`, `고릅니다`, `판단합니다`, `생성합니다` (no user outcome)

**Accelerators (EN):** `AI selects`, `the model`, `we choose`, `automatically determines`, `the system will`

**Often leakage when:** User is not told what changes for them when the system acts.

### 3. Mode jargon without benefit

Internal mode labels or restriction rationale without situational user framing.

**Accelerators (KO):** `A모드`, `B모드`, `모드에서`, `모드는`, `shallow`, `deep mode`

**Accelerators (EN):** `Mode A`, `Mode B`, `in this mode`, `mode restriction`, `lite mode`, `full mode`

**Often leakage when:** Mode name appears without "when you want to…" user situation.

### 4. Planning / meta tone

Design intent, PRD language, builder explaining architecture of the product concept.

**Accelerators (KO):** `설계상`, `기획상`, `목적은`, `의도`, `최종 목적`, `이 플로우는`, `구조상`

**Accelerators (EN):** `designed to`, `intended to`, `this flow`, `architecturally`, `philosophy`, `rationale`, `per PRD`

**Often leakage when:** Reader learns why the team built it, not what to do.

### 5. Prompt residue

LLM instruction tone leaked into UI or docs.

**Accelerators (EN):** `You are a`, `Act as`, `Respond with`, `Do not mention`, `system prompt`, role preamble blocks, chain-of-thought markers.

**Accelerators (KO):** `당신은`, `역할:`, `역할은`, `응답 형식`, `다음 형식으로`, `시스템 프롬프트`, `지시사항`, `출력 형식`

**Often leakage when:** Copy reads like instructions to the model, not to the user.

### 6. False-trust

Trust or "How it works" copy that explains mechanism instead of user control, predictability, or outcome.

**Accelerators (EN):** `we use RAG`, `embeddings`, `embedding model`, `temperature`, `chunking`, `vector store`, `model parameters`, `trained on`, `pipeline`, `retrieval-augmented`

**Accelerators (KO):** `RAG`, `임베딩`, `청킹`, `파이프라인`, `벡터`, `온도`, `모델 파라미터`, `학습하지`, `검색 증강`

**Not accelerators (too broad):** bare `we use`, bare `LLM` — use only in trust/hero context with mechanism framing, or skip grep on these alone.

**Surface priority:** trust sections, hero trust badges, privacy/security FAQ, "How it works" blocks.

**Judgment:** apply [pov-judgment.md § Trust sentence rule](./pov-judgment.md). Reframe per [rewrite-formula.md § Trust rewrites](./rewrite-formula.md).

**Often leakage when:** Reader learns how the system works internally but not what they control or can predict.

## Surfaces to grep by priority

1. Landing / marketing components (include trust badges, "How it works")
2. Onboarding and empty states
3. Widget labels, tooltips, placeholders
4. README (exclude pure code blocks; include headings and prose)
5. FAQ, error strings, metadata (`title`, `description`, OG)

## False positives (usually Pass after judgment)

- Developer README: `src/`, `pnpm`, env var names — onboarding pass
- Developer README **tech-stack / dependency mentions** (e.g. "We use Next.js", "Built with React", `pnpm install`) in install/onboarding context — Pass per Narrow Architecture Pass; not false-trust unless framed as user-facing trust mechanism
- Literal UI control labels: "Mode", "Settings" when naming a user-visible toggle the user chose
- Error codes in developer docs not shown to end users
- Third-party quoted text explicitly attributed

When in doubt, apply the checklist in [rules.md](./rules.md).