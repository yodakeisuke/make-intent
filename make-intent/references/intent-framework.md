# Intent Framework: 7要素の詳細

## 1. Objective（目的）

**定義:** 解決すべき問題と、なぜそれが重要か。定性的で aspirational。

**良い Objective の特徴:**
- 問題にフォーカス: 何が壊れているか、何が欠けているか
- なぜ重要かを説明: ビジネス価値、ユーザー影響、戦略的重要性
- トレードオフを導く: 曖昧な状況で判断を助ける

**例:**
- 弱い: "Handle customer support tickets"
- 強い: "Help customers resolve issues quickly so they can get back to work, without creating more frustration than they started with."

## 2. Desired Outcomes（望ましい成果）

**定義:** 目的が達成されたことを示す観察可能な状態。活動ではなく状態変化。

**ルール:**
- 観察可能な状態変化（エージェントの活動ではない）
- ユーザー/ステークホルダー視点（エージェント視点ではない）
- 測定可能・検証可能（エージェントの自己報告に依存しない）
- Leading（遅延しない）

**例:**
- 活動: "Respond to tickets" ← NG
- 成果: "Customer confirms their issue is resolved" ← OK

通常2〜4個が適切。それ以上はマイクロマネジメントか優先順位が不明確。

## 3. Health Metrics（健全性指標）

**定義:** 成果を追求する間に悪化させてはならないもの。

**Goodhart問題への対策:**
- "Resolve faster" → 品質低下
- "Increase throughput" → 手抜き
- "Reduce escalations" → 不適切な対応

**例:**
- CSAT 4.2以上を維持
- リピート率を上げない
- エスカレーション品質を維持

Health Metrics はハードガードレールではなくトレードオフの指針。

## 4. Strategic Context（戦略的コンテキスト）

**定義:** エージェントが動作する世界の説明。何ができるかではなく、どこにいるか。

**含めるもの:**
- System context: 他のエージェント、人間、ツール、依存関係
- Organization context: ビジネスモデル、ユーザー、ブランド
- Trade-off priorities: 例 Trust > Speed > Cost

**Strategic Context はアクションをトリガーしない。判断を inform するだけ。**

**配置の原則:**
- Core context（常に必要）: プロンプトに含める
- Reference context（時々必要）: 検索で取得
- Dynamic context（リクエストごと）: オーケストレーション層から注入

## 5. Constraints（制約）

### Steering Constraints（プロンプト層）

行動指針、リスク選好、トーン。推論に影響するが遵守を強制しない。

**例:**
- 不確かなときは確認の質問をする
- 確信度0.6-0.85の場合、不確実性を述べ安全な選択肢を提示

### Hard Constraints（オーケストレーション層）

アーキテクチャで強制。プロンプトではなくコードで実装。

**例:**
- 外部メール送信不可
- アカウント設定変更不可
- 他顧客データへのアクセス不可
- 返金や法的結果の約束不可

**重要: 制約が重要なら、言語ではなくアーキテクチャで強制する。**

## 6. Decision Types & Autonomy（決定タイプと自律性）

### 4つの自律ゾーン

| ゾーン | 説明 | 例 |
|--------|------|-----|
| Full Autonomy | 可逆、低影響範囲、理解された失敗モード | Tier-1ガイダンス、ナビゲーション |
| Guarded Autonomy | ユーザー可視変更、中リスク。ログ・ロールバック必要 | チケットタグ付け、KB記事提案 |
| Proposal-First | 戦略的・敏感な決定。提案→承認→実行 | 価格例外、アカウント変更 |
| Human-Required | 法的コミット、不可逆変更、財務アクション | 返金、契約、法的コミット |

### リスク評価の5つのレンズ

1. **Reversibility**: 元に戻せるか？
2. **Blast Radius**: 失敗時の影響範囲は？
3. **User Visibility**: ユーザーは何が起きたか理解できるか？
4. **Failure Detectability**: 失敗に気づけるか？
5. **Recovery Cost**: 修正にどれだけコストがかかるか？

## 7. Stop Rules（停止ルール）

**定義:** 実行を停止、エスカレーション、または終了すべき条件。

**Halt（停止）:**
- 矛盾する制約を検出
- 確信度が最低値を2回連続で下回る

**Escalate（エスカレーション）:**
- 定義されたスコープ外
- 法的・コンプライアンストピックを検出
- ユーザーのフラストレーションが続く

**Complete（完了）:**
- 望ましい成果を達成
- ユーザーが解決を確認

**Stop Rules は実行を終了する。トレードオフや決定品質を導くものではない。**