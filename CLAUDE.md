# dept-skills プロジェクト

## 概要

このプロジェクトは、マネージャー業務を Claude Code の Skills と Workflows で支援するシステムです。

## Skill の使い方

- `/manager-orchestrator` — 依頼内容から適切な Skill を選んで実行する
- `/manager-1on1` — 1on1 面談の準備・フォローアップ
- `/manager-evaluation` — 評価文案の作成・根拠整理
- `/manager-reporting` — 週報・KPI サマリの作成
- `/manager-risk` — リスク検知・エスカレーション整理

## 共通ルール

- すべての出力は `shared/writing-style` のルールに従うこと
- 評価・フィードバック系の出力は `shared/evidence-based-review` のルールに従うこと
- 業務原本は `docs/` を参照し、Skill 内に制度を直接書かないこと

## 出力先

| 種別 | 出力先 |
|---|---|
| 1on1 メモ | `outputs/one-on-ones/` |
| 評価ドラフト | `outputs/evaluations/` |
| 週報 | `outputs/reports/` |
| リスクメモ | `outputs/risk-notes/` |
| 下書き | `outputs/drafts/` |
