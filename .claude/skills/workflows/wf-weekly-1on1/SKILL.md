---
name: wf-weekly-1on1
description: 週次 1on1 の準備から面談後フォローアップまでを一気通貫で進める Workflow。
triggers:
  - "週次1on1"
  - "1on1の流れ全部やって"
---

# wf-weekly-1on1

## 概要

毎週の 1on1 を効率よく進めるための Workflow。
準備 → 面談 → フォローアップ の 3 フェーズをカバーする。

## フロー

```
[前日まで]
manager-orchestrator  依頼受付・対象者と目的を確認
       ↓
manager-1on1          アジェンダ・問い候補・準備シートを作成
       ↓
manager-risk          (任意) 懸念事項・リスクの事前抽出

[面談後]
manager-1on1          要点整理・アクションリストを作成
       ↓
manager-reporting     (任意) 上位者向けに 1〜2 行で要点を圧縮
       ↓
manager-task-assign   (任意) 次回アクションをタスク化
```

## 使い方

```
/wf-weekly-1on1 対象者: 田中さん、今週の状況: XXX、前回アクション: YYY
```

## チェックリスト

`checklist.md` を参照。

## 次フェーズへの引き渡し

`handoff.md` を参照。
