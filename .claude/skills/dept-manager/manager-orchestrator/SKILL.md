---
name: manager-orchestrator
description: マネージャーからの依頼を読み、適切な Skill の組み合わせと実行順序を設計する親役 Skill。
triggers:
  - "何から始めればいい"
  - "どう進めればいい"
  - "まとめてやってほしい"
---

# manager-orchestrator

## 役割

依頼内容を解釈し、どの Skill をどの順番で使うかを設計・実行する。

## 動作フロー

1. 依頼を読み、目的・対象・期限を整理する
2. 必要な Skill を特定する（下表参照）
3. 実行順序と引き渡し情報を設計する
4. 各 Skill を順番に呼び出す

## Skill 選択マップ

| 依頼の種類 | 使う Skill |
|---|---|
| 1on1 の準備・フォローアップ | `manager-1on1` |
| 評価文案・査定整理 | `manager-evaluation` |
| 週報・月報・KPI まとめ | `manager-reporting` |
| リスク・炎上・エスカレーション | `manager-risk` |
| 複合的な依頼 | 上記を組み合わせる |

## 出力フォーマット

```
【依頼の解釈】
...

【実行する Skill と順序】
1. manager-xxx: 〇〇のため
2. manager-yyy: 〇〇のため

【引き渡し情報】
- 対象者: ...
- 期間: ...
- 特記事項: ...
```
