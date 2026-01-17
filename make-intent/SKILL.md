---
name: make-intent
description: |
  LLMに渡すプロンプトとしてのIntent仕様を作成するスキル。7要素（Objective, Desired Outcomes, Health Metrics, Strategic Context, Constraints, Decision Types & Autonomy, Stop Rules）を構造化して定義する。

  Use when:
  - 「intentを作りたい」「意図を整理したい」「目的を明確にしたい」と言われたとき
  - AIエージェントやLLMへの指示を設計するとき
  - タスクの目的・制約・成功条件を構造化したいとき
  - 「何を達成したいか」が曖昧な状態から明確化したいとき
---

# Make Intent

LLMに渡すIntent仕様を作成する。ユーザーの暗黙知を引き出し、7要素を構造化する。
ここでは意図を明確化することが目的なので、具体的な解決策の考慮には踏み込まないこと。

## Process

### Phase 1: ヒアリング

ユーザーの暗黙知を引き出す。「質問する」アプローチで、ユーザー自身が気づいていない前提・判断基準・制約を明確化する。
/clarify を用いた対話を行う。前提を理解し、複数の仮説をよく考え、提案ベースで対話する。

**原則:**
- 表面的・自明な質問を避ける
- 最大3問ずつ投げる
- 仮説ベースで提案し、確認を取る
- 「十分」と判断したらPhase 2へ

**引き出すべき情報:**
- 何を解決したいか（問題の本質）
- なぜそれが重要か（ビジネス価値）
- 成功とは何か（観察可能な状態）
- 何を犠牲にできないか（トレードオフ）
- どこまで自律させるか（リスク許容度）

### Phase 2: Intent仕様作成

ヒアリングで得た情報をもとに7要素を構造化する。不確かな点は提案ベースで確認する。

**7要素の詳細は references/intent-framework.md を参照。**

## Output Format

```markdown
# Intent: [タスク名]

## 1. Objective
[解決すべき問題と、なぜそれが重要か]

## 2. Desired Outcomes
- [観察可能な成功状態1]
- [観察可能な成功状態2]
- [観察可能な成功状態3]

## 3. Health Metrics
- [悪化させてはならない指標1]
- [悪化させてはならない指標2]

## 4. Strategic Context
**System:** [他のシステム・依存関係]
**Organization:** [組織・ユーザー・ブランド]
**Trade-offs:** [優先順位: 例 Trust > Speed > Cost]

## 5. Constraints

### Steering (プロンプト層)
- [行動指針1]
- [行動指針2]

### Hard (オーケストレーション層)
- [強制的制約1]
- [強制的制約2]

## 6. Decision Types & Autonomy
- **Full Autonomy:** [完全自律可能な決定]
- **Guarded Autonomy:** [ログ・ロールバック必要な決定]
- **Proposal-First:** [提案→承認→実行の決定]
- **Human-Required:** [人間必須の決定]

## 7. Stop Rules
- **Halt:** [停止条件]
- **Escalate:** [エスカレーション条件]
- **Complete:** [完了条件]
```

## Resources

- **references/intent-framework.md**: 7要素の詳細定義と例
- **references/interview-patterns.md**: ヒアリングのパターンと質問例