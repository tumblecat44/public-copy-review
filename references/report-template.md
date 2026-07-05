# Report Template

Use for Phase 1 output and Phase 3 certification append. No target count requirement — report actual findings.

## Summary

```md
# Public Copy Review — [project or scope]

**Mode:** audit+fix | audit-only
**Scope:** [paths or surfaces]
**Date:** [ISO date]

## Counts (Phase 1 audit — historical)

| P0 | P1 | P2 | Pass (reviewed) |
|---:|---:|---:|---:|
| n  | n  | n  | n              |

## Post-fix status (Phase 2+ — certification uses these)

| Unresolved P0 (after Phase 2) | Unresolved P1 (after Phase 2) | Blocked (P0/P1) | Deferred (P2) |
|---:|---:|---:|---:|
| 0  | 0  | 0  | n              |

**Unresolved P0** = in-scope P0 findings not Status=`applied` (includes `pending`, `blocked`, or re-read still P0). Must be **0** for certification PASS.

**Surfaces scanned:** landing, README, …
**Strings reviewed:** [approx count or file count]
```

## Finding format

One block per leakage. Severity descending (P0 first).

```md
### [P0|P1|P2]-[nnn] — [short title]

- **File:** `path/to/file.tsx` (L42) or `README.md` § Section
- **Surface:** landing hero | onboarding step 2 | README architecture | …
- **Current:** `exact string or quoted excerpt`
- **Leakage type:** policy negation | system agency | mode jargon | planning/meta | prompt residue | false-trust
- **Why leakage:** [1–2 sentences: builder subject, missing benefit, etc.]
- **Proposed:** `rewritten string`
- **Benefit / action unlocked:** [what the user now understands or can do]
```

## Rewrite batch table

For Phase 2 apply — one row per edit.

| ID | File | Line/anchor | Current | Proposed | Status |
|---|---|---|---|---|---|
| P0-001 | `src/...` | L42 | `…` | `…` | pending / applied / blocked / deferred |

Status legend:
- **pending** — `audit-only` or not yet Phase 2
- **applied** — Phase 2 edit applied
- **blocked** — P0/P1 only; cannot fix without user decision; reason + escalation note required; Phase 2 incomplete
- **deferred** — P2 only; skipped with reason in notes (P0/P1 cannot use this status)

## Blockers

For incomplete `audit+fix` runs or `audit-only` reports. List every P0 (and escalated P1) not Status=`applied`.

```md
### Blockers

| ID | Severity | Reason | User escalation |
|---|---|---|---|
| P0-002 | P0 | [why blocked] | [what user must decide] |

**Unresolved P0 (after Phase 2):** [count — must be 0 for certification PASS]
```

In `audit-only` mode: all P0 findings appear here; certification PASS is not available.

## Certification block

Append after Phase 3. Run checklist from [rules.md](./rules.md).

```md
## Certification

**Result:** PASS | FAIL (with re-work list)

**PASS only if:** Unresolved P0 (after Phase 2) = 0 **and** every applied edit passes all six checklist items individually **and** every applied edit is within Phase 0 scope **and** trust auxiliary check ✓ for all trust-section edits. Phase 1 audit counts are historical; certification uses post-fix unresolved counts only. Otherwise FAIL with re-work list.

### Checklist (per edit)

Run on **each** applied edit. Aggregate row ✓ only if every edit below is ✓.

| Edit ID | Q1 User subject | Q2 Actionable | Q3 Benefit | Q4 No rationale | Q5 Trust | Q6 Same meaning | All ✓ |
|---|---|---|---|---|---|---|---|
| P0-001 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| P1-002 | ✓ | ✓ | ✓ | ✓ | N/A | ✓ | ✓ |

### Checklist (aggregate)

| # | Question | Result |
|---:|---|:---:|
| 1 | User subject (not system/team) | ✓ / ✗ |
| 2 | Actionable | ✓ / ✗ |
| 3 | Benefit visible | ✓ / ✗ |
| 4 | No internal rationale | ✓ / ✗ |
| 5 | Trust = control/predictability/outcome (see Trust auxiliary below) | ✓ / ✗ |
| 6 | Same meaning, user frame | ✓ / ✗ |

Aggregate ✓ = all applied edits passed individually in per-edit table above.

### Trust auxiliary (trust-section edits only)

For each trust-section rewrite, confirm pass/fail per [rules.md § Trust auxiliary check](./rules.md). If none, write `N/A`.

| Edit ID | Pass (control/predictability/outcome) | Fail (mechanism/policy) |
|---|---|---|
| P0-00n | ✓ | |

### Scope verification

| Applied edit ID | In Phase 0 scope? |
|---|---|
| P0-001 | ✓ / ✗ |

Any ✗ → certification FAIL.

### Post-fix verification

| Metric | Value | PASS requires |
|---|---|---|
| Unresolved P0 (after Phase 2) | 0 | = 0 |
| Unresolved P1 (after Phase 2) | 0 | = 0 (or documented blocked) |
| Blocked (P0/P1) | 0 | = 0 for PASS |

### Applied edits

List IDs where rewrite-batch **Status = applied** only; omit `pending`, `blocked`, and `deferred`.

- P0-001, P1-002, …

### Blocked (P0/P1 escalations)

- [ID, reason, user escalation] — or `none`

### Deferred (P2 only)

- [ID, reason] — or `none`

### Remaining risk

- [Any strings flagged but out of scope, or needs human product sign-off]

**Certified by:** public-copy-review Phase 3
```

## Audit-only footer

When user requested report only:

```md
---
*Audit-only mode — Phase 2/3 not run. Proposed strings are recommendations; apply via `audit+fix` or manual edit. Unresolved P0 findings are blockers — certification PASS is not available.*
```