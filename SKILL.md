---
name: public-copy-review
description: >
  Audit and rewrite public-facing copy for builder POV leakage. Detects when
  visible strings speak from the builder's perspective (policy, system internals,
  mode rationale) instead of the user's (action, benefit, outcome, control).
  Use when the user invokes /public-copy-review, asks for a public copy audit,
  mentions POV leakage or builder monologue (독백), or wants a landing/README/widget
  string review. Supports audit+fix (audit and apply) or audit-only (report only)
  when the user names either mode or says report only.
---

# Public Copy Review

**Leading principle:** Banned words are signals, not rules. The real rule is **POV leakage** — copy that reads like the builder talking to themselves instead of the user getting something done.

Universal workflow. BriefOn/Interview SaaS examples live only in reference fixtures; this skill applies to any product.

## Abstraction layers

| Layer | What it governs |
|---|---|
| **Trigger** | `/public-copy-review`, "public copy audit", POV leakage, builder monologue, 독백, landing/README/widget audit, `audit+fix`, `audit-only`, "report only" |
| **Surfaces** | Landing, README (user-facing sections), docs, widgets, onboarding, empty states, FAQ, errors, metadata |
| **Audience mapping** | UI copy → end user; README → developer onboarding (not product philosophy) |
| **Core judgment** | POV leakage types, P0/P1/P2/Pass — see [pov-judgment.md](./references/pov-judgment.md) |
| **Rewrite formula** | Internal → public conversion — see [rewrite-formula.md](./references/rewrite-formula.md) |
| **Output + Non-goals** | Report template + certification; text-only fixes; no logic/CSS/structure |

## Phase 0 — Intake

1. **Scope** — Which surfaces? Whole repo public strings, or a path list the user gave? Default: all public-facing surfaces in scope.
2. **Mode** — **`audit+fix`** (audit → apply → certify) unless the user said **`audit-only`** / **report only** → Phase 1 + report, stop. Aliases: full run = `audit+fix`; report only = `audit-only`.
3. **Audience** — Who reads each surface? Map per [pov-judgment.md § UI vs README](./references/pov-judgment.md).
4. **Load references** — Read [rules.md](./references/rules.md) for philosophy; [scan-signals.md](./references/scan-signals.md) for search accelerators; [pov-judgment.md](./references/pov-judgment.md) before classifying any finding.

**Completion:** Scope, mode, and audience map are explicit before Phase 1 starts.

## Phase 1 — Audit

Goal: find every **POV leakage** instance in visible strings. No forced hit count — report what you find.

### 0. Enumerate surfaces

From Phase 0 scope, list every file and surface to audit (landing components, README sections, widget strings, etc.). Record in the report **Surfaces scanned** field. Do not grep repo-wide until this list exists.

### 1. Scan

1. Grep using signal categories in [scan-signals.md](./references/scan-signals.md) within enumerated files only — signals accelerate search; they are **not** final judgment.
2. **Also read all visible strings** in scoped files even when grep returns nothing. Leakage often hides in benign-looking prose.
3. For each candidate string, apply [pov-judgment.md](./references/pov-judgment.md) — classify P0 / P1 / P2 / Pass.

### 2. README narrow architecture pass

When auditing README (or docs labeled "architecture"):

- **PASS:** folder structure, module locations, data flow for onboarding, run/deploy/env/edit points.
- **NOT PASS (P0/P1):** product philosophy, mode restriction rationale, AI judgment criteria, PRD design intent — even if the section is titled architecture.

Hard rule detail: [pov-judgment.md § README Narrow Architecture Pass](./references/pov-judgment.md).

### 3. Trust copy check

Trust sections must sell **control, predictability, outcome** — not system/AI internals. P0/P1 if mechanism is exposed. See [rules.md § Trust auxiliary](./references/rules.md) and [pov-judgment.md § Trust sentence rule](./references/pov-judgment.md).

### 4. Produce report

Format per [report-template.md](./references/report-template.md):

- Summary counts (P0/P1/P2/Pass) — no target count required
- One finding per leakage: file, surface, current, why leakage, proposed, benefit/action unlocked
- Rewrite batch table for Phase 2

**Completion:** Every scoped visible string is read or grep-touched; each leakage is classified and logged. If `audit-only`, deliver report and stop — list unresolved P0 findings under **Blockers** (certification PASS is not available; Phase 2/3 do not run).

## Phase 2 — Apply (text-only)

Skip if `audit-only`.

1. Apply in severity order: **P0 first, then P1, then P2** (if not deferred).
2. Apply **proposed** strings from the rewrite batch table only — string replacements in user-facing files.
3. Use [rewrite-formula.md](./references/rewrite-formula.md) when refining proposals before edit.
4. Do **not** change component structure, logic, CSS, routing, or props — copy only.
5. Do **not** edit internal spec docs (PRD, ADR, agent briefs, `.scratch/` specs) unless they are themselves a public surface the user scoped.

**Completion:** Every in-scope **P0 and P1** finding has rewrite-batch Status = `applied`, or Status = `blocked` with reason and user escalation noted in report **Blockers** (Phase 2 incomplete until resolved). **Only P2** may use Status = `deferred`. After apply, record **Unresolved P0 (after Phase 2)** in the report summary — must be 0 before Phase 3. Aligns with [pov-judgment.md § P0/P1/P2](./references/pov-judgment.md).

## Phase 3 — Certification

1. Re-read changed strings in context (surrounding UI, not isolated lines).
2. Run the **Final Review Checklist** from [rules.md](./references/rules.md) on **each** applied rewrite; record per-edit results in the certification block (aggregate ✓ only if every applied edit passed individually).
3. For any **trust-section** edit, also run the **Trust auxiliary check** table from [rules.md § Trust auxiliary check](./references/rules.md).
4. Confirm no new leakage introduced (e.g. swapped builder jargon for different builder jargon).
5. **Scope gate:** confirm every applied edit maps to a file/surface from Phase 0 enumeration; any out-of-scope touch → certification **FAIL**.
6. Append certification block to report per [report-template.md](./references/report-template.md).

**Completion:** Certification **PASS** only if: (a) every applied edit passes all six checklist items individually; (b) trust auxiliary passes for trust edits; (c) **Unresolved P0 (after Phase 2) = 0** — meaning every in-scope P0 rewrite-batch row is `applied` (not `pending` or `blocked`) and re-read strings pass judgment with no remaining P0 leakage; (d) no out-of-scope edits. List any deferred **P2** items. Phase 1 audit counts (e.g. P0 = 3) are historical; certification uses post-fix unresolved counts only.

## Non-goals

- **No logic/structure/CSS changes** in Phase 2 — text replacements only.
- **No editing internal spec docs** unless explicitly scoped as public.
- **No forced hit counts** during audit — quality of judgment over volume.
- **Not prettier prose** — goal is user-facing interface (action, benefit, outcome), not literary polish.
- **Not a banned-word linter** — signals in scan-signals.md require context judgment.

## Quick reference pointers

| Need | File |
|---|---|
| Philosophy + checklist | [references/rules.md](./references/rules.md) |
| P0/P1/P2 + README/trust hard rules | [references/pov-judgment.md](./references/pov-judgment.md) |
| Grep accelerators (not rules) | [references/scan-signals.md](./references/scan-signals.md) |
| Rewrite patterns + fixtures | [references/rewrite-formula.md](./references/rewrite-formula.md) |
| Report + certification format | [references/report-template.md](./references/report-template.md) |