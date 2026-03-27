# dept-skills 構成ガイド

## 推奨ディレクトリ構成

```
project-root/
├── CLAUDE.md
├── .claude/
│   ├── settings.json
│   ├── skills/
│   │   ├── dept-manager/
│   │   │   ├── manager-orchestrator/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── templates/
│   │   │   │   │   ├── task-routing.md
│   │   │   │   │   └── execution-plan.md
│   │   │   │   └── examples/
│   │   │   │       └── routing-example.md
│   │   │   ├── manager-decision/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── templates/
│   │   │   │   │   ├── option-compare.md
│   │   │   │   │   └── decision-note.md
│   │   │   │   └── examples/
│   │   │   │       └── decision-sample.md
│   │   │   ├── manager-1on1/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── templates/
│   │   │   │   │   ├── agenda.md
│   │   │   │   │   ├── prep-sheet.md
│   │   │   │   │   └── followup-note.md
│   │   │   │   └── examples/
│   │   │   │       └── one-on-one-sample.md
│   │   │   ├── manager-evaluation/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── templates/
│   │   │   │   │   ├── evaluation-draft.md
│   │   │   │   │   ├── evidence-summary.md
│   │   │   │   │   └── feedback-comment.md
│   │   │   │   └── examples/
│   │   │   │       └── evaluation-sample.md
│   │   │   ├── manager-reporting/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── templates/
│   │   │   │   │   ├── weekly-report.md
│   │   │   │   │   ├── executive-summary.md
│   │   │   │   │   └── kpi-status.md
│   │   │   │   └── examples/
│   │   │   │       └── reporting-sample.md
│   │   │   ├── manager-task-assign/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── templates/
│   │   │   │   │   ├── task-breakdown.md
│   │   │   │   │   ├── assignment-sheet.md
│   │   │   │   │   └── priority-matrix.md
│   │   │   │   └── examples/
│   │   │   │       └── task-assign-sample.md
│   │   │   └── manager-risk/
│   │   │       ├── SKILL.md
│   │   │       ├── templates/
│   │   │       │   ├── risk-register.md
│   │   │       │   ├── escalation-note.md
│   │   │       │   └── mitigation-plan.md
│   │   │       └── examples/
│   │   │           └── risk-sample.md
│   │   ├── workflows/
│   │   │   ├── wf-weekly-1on1/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── checklist.md
│   │   │   │   └── handoff.md
│   │   │   ├── wf-quarterly-evaluation/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── checklist.md
│   │   │   │   └── handoff.md
│   │   │   ├── wf-weekly-reporting/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── checklist.md
│   │   │   │   └── handoff.md
│   │   │   ├── wf-incident-response/
│   │   │   │   ├── SKILL.md
│   │   │   │   ├── checklist.md
│   │   │   │   └── handoff.md
│   │   │   └── wf-project-kickoff/
│   │   │       ├── SKILL.md
│   │   │       ├── checklist.md
│   │   │       └── handoff.md
│   │   └── shared/
│   │       ├── writing-style/
│   │       │   └── SKILL.md
│   │       ├── meeting-output/
│   │       │   └── SKILL.md
│   │       └── evidence-based-review/
│   │           └── SKILL.md
│   ├── subagents/
│   │   ├── planning-agent.md
│   │   ├── reviewer-agent.md
│   │   └── reporting-agent.md
│   ├── hooks/
│   │   ├── pre-tool-use.sh
│   │   ├── post-tool-use.sh
│   │   └── notify-summary.sh
│   └── memory/
│       ├── organization-glossary.md
│       ├── manager-principles.md
│       └── recurring-patterns.md
├── docs/
│   ├── policies/
│   │   ├── evaluation-policy.md
│   │   ├── one-on-one-policy.md
│   │   ├── escalation-policy.md
│   │   └── reporting-policy.md
│   ├── org/
│   │   ├── team-structure.md
│   │   ├── role-definition.md
│   │   └── decision-authority.md
│   ├── workflows/
│   │   ├── weekly-1on1-flow.md
│   │   ├── quarterly-evaluation-flow.md
│   │   ├── incident-response-flow.md
│   │   └── reporting-flow.md
│   └── templates/
│       ├── 1on1-template.md
│       ├── evaluation-template.md
│       ├── weekly-report-template.md
│       └── risk-template.md
├── data/
│   ├── members/
│   ├── projects/
│   ├── kpis/
│   └── incidents/
├── outputs/
│   ├── drafts/
│   ├── reports/
│   ├── evaluations/
│   ├── one-on-ones/
│   └── risk-notes/
└── scripts/
    ├── collect_kpi.py
    ├── summarize_meeting.py
    └── validate_output.py
```

---

## 構成の意図

| 層 | 役割 |
|---|---|
| `dept-manager/` | 機能別の単機能 Skill 群 |
| `workflows/` | 複数 Skill を束ねる業務シナリオ |
| `shared/` | 全 Skill 共通の出力ルール |

Claude Code の Skills は関連時に自動適用・明示呼び出しの両方ができ、subagents は専用コンテキストと役割分担に向いています。機能分割と業務フロー分割を分けることで、相性の良い設計になります。

---

## dept-manager の各 Skill

`dept-manager` の 7 Skill はそれぞれ単機能の専門家です。

| Skill | 担当内容 |
|---|---|
| `manager-orchestrator` | 依頼を読み、どの Skill を使うべきか決め、順番を設計する親役 |
| `manager-decision` | 選択肢比較・判断理由整理・意思決定メモ作成 |
| `manager-1on1` | 面談準備・問いの生成・フォローアップ整理 |
| `manager-evaluation` | 評価文案・根拠整理・観察と解釈の分離 |
| `manager-reporting` | 週報・月報・役員向け要約・KPI 整理 |
| `manager-task-assign` | タスク分解・優先順位付け・担当割り当て案 |
| `manager-risk` | リスク検知・炎上予兆・エスカレーション整理 |

---

## workflows の設計

`workflows` は「1 Skill = 1 責務」ではなく、複数 Skill をどう連携させるかの手順書です。

### wf-weekly-1on1

1. `manager-orchestrator` が依頼を受ける
2. `manager-1on1` が面談準備資料を作る
3. 必要なら `manager-risk` が懸念点を抽出
4. 面談後は `manager-reporting` が要点を短くまとめる
5. 次回アクションがあれば `manager-task-assign` が整理する

### wf-quarterly-evaluation

1. `manager-orchestrator` が評価対象と期間を整理
2. `manager-evaluation` が証拠ベースでドラフト作成
3. `manager-decision` が昇格・重点育成・配置転換などの判断整理
4. `manager-reporting` が上位者向けの短い説明資料に落とす

### wf-incident-response

1. 事象整理
2. `manager-risk` で影響と再発リスク評価
3. `manager-decision` で対応方針案
4. `manager-reporting` で関係者共有文を作成

---

## 命名ルール

| 種別 | 命名パターン | 例 |
|---|---|---|
| 機能 Skill | `manager-xxx` | `manager-1on1` |
| 業務 Workflow | `wf-xxx` | `wf-weekly-1on1` |
| 共通 Skill | 用途単位のフォルダ名 | `writing-style` |
| テンプレート | `templates/*.md` | `templates/agenda.md` |
| 例 | `examples/*.md` | `examples/routing-example.md` |

見た瞬間に「専門機能」「業務シナリオ」「共通ルール」が判別できます。

---

## 運用しやすくするための設計ポイント

### 1. shared を必ず置く

評価や 1on1 は書きぶりがばらつくと運用品質が落ちます。`shared/writing-style` や `shared/evidence-based-review` を置き、すべての `manager` 系 Skill がそれを参照する形にします。CLAUDE.md や memory で行動ルールを持たせる考え方とも相性が良いです。

### 2. 業務原本は docs 側に置く

SKILL.md に制度を全部書かず、`docs/policies` に原本を置き、Skill はそこを参照するだけにします。制度変更時に 1 か所直せば済みます。

### 3. outputs を分ける

1on1・評価・週報・リスクメモを同じ場所に出すとすぐ散らかります。出力先を分けるだけでレビューと再利用が楽になります。

### 4. hooks は最小限で良い

Claude Code は hooks で特定タイミングの処理を差し込めますが、最初から複雑化しすぎると管理が大変です。まずは「出力の検証」「完了通知」「ログ整形」くらいが現実的です。

---

## 最初に作るべき最小セット

全部一気に作るより、まずはこの構成で十分です。

```
.claude/skills/
├── dept-manager/
│   ├── manager-orchestrator/
│   ├── manager-1on1/
│   ├── manager-evaluation/
│   ├── manager-reporting/
│   └── manager-risk/
├── workflows/
│   ├── wf-weekly-1on1/
│   └── wf-quarterly-evaluation/
└── shared/
    ├── writing-style/
    └── evidence-based-review/
```

この 5 Skill + 2 Workflow + 2 shared で、**1on1・評価・週報** の 3 本柱が回せます。
