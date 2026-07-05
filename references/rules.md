# Public-Facing Writing Rules

Philosophy for all public surfaces. Judgment criteria live in [pov-judgment.md](./pov-judgment.md); conversion patterns in [rewrite-formula.md](./rewrite-formula.md).

## Core rule

**Write from the user's POV, not the builder's.**

The user cares about:
- **Action** — what they do next
- **Benefit** — what they gain
- **Outcome** — what they get at the end
- **Control / predictability** — what will happen, what they can change

The builder cares about (and must not leak into public copy):
- Product strategy and positioning rationale
- Mode restrictions and why modes exist
- AI/system decision logic
- PRD design intent and trade-offs
- Internal policy stated as negation ("we don't…", "하지 않습니다")

If a sentence only makes sense to someone who built the product, it is POV leakage.

## Public surfaces

Audit these when in scope:

| Surface | Examples |
|---|---|
| Landing / marketing | Hero, features, pricing, trust, CTA |
| README (user-facing) | Quick start, install, folder map, env — not philosophy |
| Docs | User guides, API consumer docs, changelog user notes |
| Widgets / embeds | Labels, tooltips, placeholders visible to end users |
| Onboarding | First-run copy, step labels, coach marks |
| Empty states | Zero-data messages, "nothing here yet" |
| FAQ | Questions users ask, not design rationale |
| Errors (user-visible) | Toast, inline validation, 4xx/5xx user messages |
| Metadata | `title`, `description`, OG tags, app store strings |

## Forbidden sentence types

These are **types**, not keyword bans. Context determines severity (see pov-judgment).

1. **Product strategy** — why the product is shaped this way for the market
2. **Internal policy** — what the team decided not to build or not to do
3. **System prompt residue** — instructions that belonged in an LLM prompt, not UI
4. **Mode jargon without benefit** — A/B mode labels, internal mode names, restriction rationale
5. **Planning / meta tone** — "we designed…", "this feature is intended to…", "설계상…"
6. **AI agency exposure** — "AI chooses…", "the model decides…" without user-facing framing
7. **False-trust copy** — claiming trust by explaining internals instead of user control

## Bad vs good (English)

Illustrative rows only. Full before/after fixtures (KO + EN) are SSOT in [rewrite-formula.md](./rewrite-formula.md).

| Bad (builder POV) | Good (user POV) |
|---|---|
| The AI selects the next question based on your answers. | Your answers shape what gets asked next — no repeat questions. |
| We don't go deep on feature design in Mode A. | Start from your workflow — get app ideas you can use right away. |

More examples: [rewrite-formula.md § English fixtures](./rewrite-formula.md).

## Final review checklist

Run on every rewrite before certification:

1. **User subject** — Is the user (or their outcome) the grammatical subject, not the system or the team?
2. **Actionable** — Can the reader tell what to do or what happens next?
3. **Benefit visible** — Is the gain stated, not just the mechanism?
4. **No internal rationale** — Would a user who never read the PRD still understand and care?
5. **Trust = control** — If it's trust copy, does it promise predictability/outcome, not AI internals?
6. **Same meaning, user frame** — Did we reframe without changing product behavior claims?

All six must pass for certification. A single fail on a **P0/P1** rewrite → revise before certifying (cannot defer). A **P2** rewrite may be deferred with explicit reason.

## Trust auxiliary check

Trust copy (security, privacy, AI reliability sections) must answer: **"What can I control? What can I predict? What outcome do I get?"**

| Pass | Fail |
|---|---|
| You choose what to share before anything runs. | We use a RAG pipeline with chunking and embeddings. |
| You'll see the same questions in the same order every time. | The LLM temperature is set low for consistency. |
| Your data stays in your project until you export. | We don't train on your inputs (internal policy negation). |

Mechanism-only trust copy is P0/P1 leakage even in a "Trust" or "How it works" section. Reframe per [rewrite-formula.md § Trust rewrites](./rewrite-formula.md).