---
name: wf-quarterly-evaluation
description: 四半期評価の証拠収集から上位者向け説明資料作成までを一気通貫で進める Workflow。
triggers:
  - "四半期評価"
  - "評価の流れ全部やって"
  - "査定"
---

# wf-quarterly-evaluation

## 概要

四半期ごとの評価プロセスを効率化する Workflow。
証拠収集 → 評価ドラフト → 判断整理 → 上位者向け資料 の 4 フェーズをカバーする。

## フロー

```
manager-orchestrator  評価対象者・期間・評価観点を整理
       ↓
manager-evaluation    証拠ベースで評価ドラフトを作成
       ↓
manager-decision      昇格・重点育成・配置転換などの判断を整理
       ↓
manager-reporting     上位者向けの短い説明資料を作成
```

## 使い方

```
/wf-quarterly-evaluation
対象者: 田中さん、期間: 2025 Q1、観察事実: XXX
```

## チェックリスト

`checklist.md` を参照。

## 次フェーズへの引き渡し

`handoff.md` を参照。
