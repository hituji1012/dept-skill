# dept-skills

マネージャー業務を Claude Code の Skills と Workflows で支援するサンプルプロジェクトです。

---

## 現在の構成

```
dept-skills/
├── CLAUDE.md
├── .claude/
│   └── skills/
│       ├── dept-manager/
│       │   ├── manager-orchestrator/   # 依頼を読み、適切な Skill を選んで実行
│       │   ├── manager-1on1/           # 面談準備・問いの生成・フォローアップ
│       │   ├── manager-evaluation/     # 評価文案・根拠整理
│       │   ├── manager-reporting/      # 週報・KPI サマリ
│       │   └── manager-risk/           # リスク検知・エスカレーション整理
│       ├── workflows/
│       │   ├── wf-weekly-1on1/         # 週次 1on1 の一連フロー
│       │   └── wf-quarterly-evaluation/# 四半期評価の一連フロー
│       └── shared/
│           ├── writing-style/          # 全 Skill 共通の出力スタイル
│           └── evidence-based-review/  # 評価・フィードバック系の共通ルール
├── team_data/
│   ├── A/   # メンバー A のサンプルデータ（キャリア目標・業務計画・スケジュール）
│   └── B/   # メンバー B のサンプルデータ
└── outputs/
    ├── one-on-ones/   # 1on1 準備メモの出力先
    ├── evaluations/   # 評価ドラフトの出力先
    ├── reports/       # 週報の出力先
    └── risk-notes/    # リスクメモの出力先
```

---

## サンプルの動作手順

このリポジトリには架空のチームメンバー A・B のサンプルデータが同梱されています。
以下の手順で、Skills がどう動くかをすぐに確認できます。

### 前提

- Claude Code がインストール済みであること（`claude` コマンドが使えること）
- このリポジトリの **ルートで** `claude` を起動すること

### Step 1: サンプルデータを確認する

`team_data/A/` 以下の 3 ファイルを開いてメンバー A の情報を確認してください。

| ファイル | 内容 |
|---|---|
| `career-goals.md` | キャリア目標 |
| `term-job-plan.md` | 期の業務計画 |
| `monthly-schedule.md` | 月次スケジュール |

### Step 2: 1on1 準備を生成する

Claude Code のチャットで以下のように入力してください。

```
/manager-1on1 Aさんの1on1準備をお願いします
```

`outputs/one-on-ones/` に準備メモが生成されます。
生成済みのサンプル出力は [outputs/one-on-ones/2026-03-28_A.md](outputs/one-on-ones/2026-03-28_A.md) で確認できます。

### Step 3: ワークフロー全体を試す

週次 1on1 ワークフローをまとめて実行する場合：

```
/wf-weekly-1on1
```

面談準備 → リスク抽出 → 要点まとめ → ネクストアクション整理、の一連の流れが動きます。

### Tips

- メンバーを追加するには `team_data/<名前>/` を作り、同じ 3 ファイルを置くだけです
- 出力のトーンや形式を変えたい場合は `.claude/skills/shared/writing-style/SKILL.md` を編集してください
- 制度・ポリシーは `docs/policies/` に置き、Skill 内には書かないのが推奨です（後述）

---

## 発展させるとしたら

現在は最小構成ですが、以下の方向に拡張できます。

### 追加できる Skill

| Skill | 担当内容 |
|---|---|
| `manager-decision` | 選択肢比較・判断理由整理・意思決定メモ |
| `manager-task-assign` | タスク分解・優先順位付け・担当割り当て案 |

### 追加できるワークフロー

| Workflow | 内容 |
|---|---|
| `wf-incident-response` | 事象整理 → リスク評価 → 対応方針 → 関係者共有文 |
| `wf-project-kickoff` | キックオフ準備 → タスク分解 → リスク洗い出し |
| `wf-weekly-reporting` | KPI 収集 → 週報生成 → 役員向け要約 |

### docs/ で制度を一元管理する

```
docs/
├── policies/
│   ├── evaluation-policy.md
│   ├── one-on-one-policy.md
│   └── escalation-policy.md
└── org/
    ├── team-structure.md
    └── role-definition.md
```

SKILL.md に制度を直接書かず `docs/policies/` に原本を置くと、制度変更時に 1 か所直すだけで済みます。

### hooks で自動化する

Claude Code は hooks で特定タイミングの処理を差し込めます。まずは以下 3 つが現実的です。

| hooks | 用途 |
|---|---|
| `pre-tool-use` | 出力先のディレクトリ存在確認 |
| `post-tool-use` | 完了通知・ログ整形 |
| `notify-summary` | 面談後の Slack 通知など |

### subagents で役割分担する

複雑なワークフローでは subagents に専用コンテキストを持たせると整理しやすくなります。

| agent | 役割 |
|---|---|
| `planning-agent` | タスク設計・優先順位判断 |
| `reviewer-agent` | 出力の品質チェック |
| `reporting-agent` | サマリ生成・整形 |
