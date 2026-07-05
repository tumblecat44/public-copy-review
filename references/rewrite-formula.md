# Rewrite Formula

Convert **internal / builder** framing to **public / user** framing. Judgment types in [pov-judgment.md](./pov-judgment.md).

## Internal → public conversion

```
[Builder subject] + [policy/mechanism]     →  [User subject] + [action/benefit/outcome]
[System/AI] + [opaque verb]                →  [User] + [what changes for them]
[Mode label] + [restriction]               →  [Situation] + [what they get]
[Negation] + [what we don't do]            →  [Affirmation] + [what they do get]
[Trust via mechanism]                      →  [Trust via control/predictability/outcome]
```

### Rewrite steps

1. **Identify leakage type** (policy, agency, mode, meta, prompt, false-trust).
2. **Extract user outcome** — what does the user get, do, or control?
3. **Flip subject** — user or their outcome as grammatical subject.
4. **Remove builder-only clauses** — PRD rationale, mode letters, pipeline detail.
5. **Check trust** — if trust copy, swap mechanism for control/predictability.
6. **Verify** — run Final Review Checklist in [rules.md](./rules.md).

## Korean fixtures (approved table)

| Before (builder) | After (user) |
|---|---|
| A모드에서 너무 깊게 들어가지 않습니다 | 말한 업무 흐름에서 바로 쓸 수 있는 앱 아이디어를 먼저 찾습니다 |
| 고정 30문항 설문입니다 | 필요한 것만 물어봐서 같은 질문을 반복하지 않습니다 |
| AI가 다음 질문을 고른다 | 답변에 맞춰 다음 질문이 달라집니다 |
| 기능 설계는 깊게 하지 않습니다 | 후보를 고르면 그때 필요한 기능을 함께 구체화합니다 |
| 필수 기능 vs 나중 기능 분리 | 첫 버전에 꼭 필요한 것부터 정리합니다 |
| 브리프가 최종 목적입니다 | 인터뷰가 끝나면 개발을 시작할 수 있는 문서를 받습니다 |

## English fixtures

| Before (builder) | After (user) |
|---|---|
| We don't go deep on features in Mode A. | Start from your workflow — get app ideas you can use right away. |
| This is a fixed 30-question survey. | We only ask what's needed — no repeat questions. |
| The AI picks the next question. | Your answers shape what gets asked next — no repeat questions. |
| We don't design features deeply upfront. | When you pick a direction, we flesh out the features that matter. |
| We separate must-have vs later features. | We start with what your first version actually needs. |
| The brief is the end goal. | When you finish, you get a document ready to start development. |

## Trust rewrites

| Before (false-trust) | After (control / predictability / outcome) |
|---|---|
| AI가 다음 질문을 고릅니다 | 답변에 맞춰 필요한 질문만 이어집니다 |
| Low-temperature model for consistency | You'll get the same follow-ups when you give the same answers |
| We use RAG over your uploads | Answers pull from what you uploaded — nothing outside your project |
| We don't train on your data | Your inputs stay in your session until you delete them |
| Dynamic question graph | No question repeats once you've answered it |

Pattern: **name what the user can predict or control**, not how the system implements it.

## Mode name translation

Replace internal mode labels with **situation-based user choice**.

| Avoid | Prefer |
|---|---|
| Mode A / A모드 | When you want ideas fast from your workflow / 업무 흐름에서 바로 아이디어를 원할 때 |
| Mode B / B모드 | When you want to explore one idea in depth / 하나를 깊게 다듬고 싶을 때 |
| Lite / Full | Start quick / Go deeper (tie to user goal, not tier name) |

If the UI must show a mode toggle, pair the label with a **one-line user situation**, not restriction rationale.

## Patterns by leakage type

### Policy negation → user benefit

- Before: `~하지 않습니다` as main message
- After: Lead with what **does** happen; drop the negation if redundant

### System agency → user-visible change

- Before: `AI가 ~합니다`
- After: `~하면 ~가 달라집니다` / `your answers shape ~`

### Planning meta → action

- Before: `이 기능은 ~을 위해 설계되었습니다`
- After: `~하려면 ~하세요` / `~하면 ~를 받습니다`

### README philosophy → narrow architecture

- Before: Paragraph on why shallow-first ideation
- After: `src/interview/` — question flow; edit `questions.ts` to change order