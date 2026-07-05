# Public Copy Review

[![skills.sh](https://skills.sh/b/tumblecat44/public-copy-review)](https://skills.sh/tumblecat44/public-copy-review)

Audit and rewrite public-facing copy for **builder POV leakage** — when visible strings sound like the builder talking to themselves (policy, system internals, mode rationale) instead of the user getting something done (action, benefit, outcome, control).

Works on landing pages, README user-facing sections, widgets, onboarding, empty states, FAQ, errors, and metadata.

## Quickstart

1. Run the skills.sh installer:

```bash
npx skills@latest add tumblecat44/public-copy-review
```

2. Pick your coding agent (Cursor, Claude Code, Codex, etc.) and install.

3. Run the skill:

```
/public-copy-review
```

Or ask naturally: "public copy audit", "POV leakage", "builder monologue", "독백".

## Modes

- **`audit+fix`** (default) — audit → rewrite copy → certify
- **`audit-only`** — report only, no edits

## What it checks

- Landing and marketing copy
- README sections meant for users (not internal architecture philosophy)
- Trust sections (control and outcome, not AI/system internals)
- Widget, onboarding, and error strings

Banned words are signals, not rules. The real judgment is POV leakage — see [SKILL.md](./SKILL.md) and [references/](./references/).

## Reference

- **[SKILL.md](./SKILL.md)** — main workflow (audit → apply → certify)
- **[references/rules.md](./references/rules.md)** — philosophy + checklist
- **[references/pov-judgment.md](./references/pov-judgment.md)** — P0/P1/P2 classification
- **[references/rewrite-formula.md](./references/rewrite-formula.md)** — rewrite patterns
- **[references/scan-signals.md](./references/scan-signals.md)** — grep accelerators
- **[references/report-template.md](./references/report-template.md)** — report format