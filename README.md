# delta-agents

deltaシステムで採用するエージェント定義の原本リポジトリ。

## 構造

```
agents/
├── design/              # デザイン
├── engineering/         # エンジニアリング
├── marketing/           # マーケティング
├── operations/          # オペレーション
├── planning/            # 企画立案
├── product/             # プロダクト
├── project-management/  # プロジェクト管理
├── quality/             # 品質管理・セキュリティ監査
└── testing/             # テスト・QA

docs/
├── agents.md            # 全エージェントのキャラクター紹介
├── writing-guide.md     # エージェント定義の書き方
└── sample-agent.md      # サンプル定義
```

`agents/` ディレクトリをそのまま `~/.claude/agents/` にコピーして使える。

## セットアップ

### 1. エージェントファイルの配置

Claude Code のカスタムエージェントはサブディレクトリに対応していないため、全ファイルをフラットにコピーする。

```bash
# 既存のエージェントがあれば退避
# cp -r ~/.claude/agents/ ~/.claude/agents.bak/

# 全エージェントをフラットにコピー
find agents/ -name '*.md' -exec cp {} ~/.claude/agents/ \;
```

### 2. キャラ名での呼び出し設定（任意）

各エージェントにはキャラクター名が設定されている（[docs/agents.md](docs/agents.md) 参照）。キャラ名やキーワードでエージェントを呼び出したい場合は、マッピングファイルを作成して `CLAUDE.md` から参照する。

**`~/.claude/callagent.md`** にマッピングを記述:

```markdown
# エージェント呼び出しルール

ユーザーの依頼が以下のキーワード・キャラ名に該当する場合、対応するエージェントを呼び出すこと。

| キャラ名 / トリガー | エージェント（subagent_type） |
|---------------------|-------------------------------|
| メフィ / セキュリティ検証 | security-auditor |
| アテナ / コードレビュー | code-reviewer |
| ...                 | ...                           |
```

**`~/.claude/CLAUDE.md`** に一行追加:

```markdown
@~/.claude/callagent.md
```

これで「メフィーチェックして」「アテナにレビュー頼んで」のようにキャラ名で呼び出せるようになる。

## エージェント定義フォーマット

各エージェントは `.md` ファイルで定義する。詳細は [docs/writing-guide.md](docs/writing-guide.md) を参照。

```markdown
---
name: エージェント名
description: 一行の説明
tools: 使用可能なツール（カンマ区切り）
model: 使用モデル
---

（エージェントのプロンプト本文）
```

## エージェント一覧（全36体）

### Design（デザイン）

| 名前 | 説明 |
|------|------|
| [brand-guardian](agents/design/brand-guardian.md) | ブランドの一貫性を守る。ガイドライン策定・運用、トーン&マナー管理 |
| [ui-designer](agents/design/ui-designer.md) | UIデザインの設計・レビュー。コンポーネント設計、デザインシステム構築 |
| [ux-researcher](agents/design/ux-researcher.md) | UXリサーチの設計・実施。ユーザビリティテスト、ペルソナ作成 |
| [visual-storyteller](agents/design/visual-storyteller.md) | ビジュアルストーリーテリング。データビジュアライゼーション、プレゼン資料 |

### Engineering（エンジニアリング）

| 名前 | 説明 |
|------|------|
| [ai-engineer](agents/engineering/ai-engineer.md) | AI/ML機能の設計・実装。LLM統合、プロンプトエンジニアリング、RAG構築 |
| [backend-architect](agents/engineering/backend-architect.md) | バックエンドの設計・実装。API設計、DB設計、マイクロサービス構成 |
| [devops-automator](agents/engineering/devops-automator.md) | CI/CD、インフラ自動化。GitHub Actions、Docker、Terraform等 |
| [frontend-developer](agents/engineering/frontend-developer.md) | フロントエンド開発。React、Vue、Next.js等のUI構築 |
| [mobile-app-builder](agents/engineering/mobile-app-builder.md) | モバイルアプリ開発。React Native、Flutter、Swift、Kotlin等 |
| [rapid-prototyper](agents/engineering/rapid-prototyper.md) | アイデアの高速プロトタイピング。最小構成で動くものを素早く作る |

### Marketing（マーケティング）

| 名前 | 説明 |
|------|------|
| [app-store-optimizer](agents/marketing/app-store-optimizer.md) | ASO（アプリストア最適化）。メタデータ最適化、キーワード戦略 |
| [content-creator](agents/marketing/content-creator.md) | コンテンツの企画・制作。ブログ、ニュースレター、LP、プレスリリース |
| [growth-hacker](agents/marketing/growth-hacker.md) | グロースハック戦略。ファネル分析、A/Bテスト設計、バイラル施策 |
| [instagram-curator](agents/marketing/instagram-curator.md) | Instagramのコンテンツキュレーション。フィード設計、ストーリーズ戦略 |
| [reddit-community-builder](agents/marketing/reddit-community-builder.md) | Redditでのコミュニティ構築。サブレディット運営、投稿戦略 |
| [tiktok-strategist](agents/marketing/tiktok-strategist.md) | TikTokマーケティング戦略。トレンド分析、コンテンツ企画 |
| [twitter-engager](agents/marketing/twitter-engager.md) | X（Twitter）エンゲージメント戦略。ツイート作成、コミュニティ運営 |

### Operations（オペレーション）

| 名前 | 説明 |
|------|------|
| [analytics-reporter](agents/operations/analytics-reporter.md) | データ分析とレポート作成。KPIダッシュボード設計、インサイト提供 |
| [finance-tracker](agents/operations/finance-tracker.md) | 財務管理とコスト追跡。予算管理、クラウド費用最適化 |
| [infrastructure-maintainer](agents/operations/infrastructure-maintainer.md) | インフラの運用・保守。監視、障害対応、パフォーマンスチューニング |
| [legal-compliance-checker](agents/operations/legal-compliance-checker.md) | 法務・コンプライアンスチェック。利用規約、ライセンス確認 |
| [support-responder](agents/operations/support-responder.md) | カスタマーサポート対応。問い合わせドラフト作成、FAQ整備 |

### Planning（企画立案）

| 名前 | 説明 |
|------|------|
| [strategic-advisor](agents/planning/strategic-advisor.md) | 戦略相談役。計画の壁打ち、意思決定の整理、リスク評価 |

### Product（プロダクト）

| 名前 | 説明 |
|------|------|
| [feedback-synthesizer](agents/product/feedback-synthesizer.md) | ユーザーフィードバックの収集・統合・分析。インサイト抽出 |
| [sprint-prioritizer](agents/product/sprint-prioritizer.md) | スプリント計画と優先度付け。バックログ整理、タスク見積もり |
| [trend-researcher](agents/product/trend-researcher.md) | 市場トレンドや競合の調査・分析。技術トレンド、ユーザー動向 |

### Project Management（プロジェクト管理）

| 名前 | 説明 |
|------|------|
| [experiment-tracker](agents/project-management/experiment-tracker.md) | 実験・仮説検証のトラッキング。A/Bテスト管理、結果分析 |
| [product-shipper](agents/project-management/product-shipper.md) | リリース管理。リリース計画、チェックリスト、ローンチ準備 |
| [studio-producer](agents/project-management/studio-producer.md) | プロジェクト全体のプロデュース。スケジュール管理、リソース配分 |

### Quality（品質管理）

| 名前 | 説明 |
|------|------|
| [code-reviewer](agents/quality/code-reviewer.md) | コードレビュー担当。可読性・保守性・バグ検出・セキュリティ観点で包括レビュー |
| [security-auditor](agents/quality/security-auditor.md) | CCO/セキュリティ監査役。デビルズアドボケートとして設計・コードに鋭くツッコむ |

### Testing（テスト・QA）

| 名前 | 説明 |
|------|------|
| [api-tester](agents/testing/api-tester.md) | APIテスト。エンドポイント検証、負荷テスト、テスト自動化 |
| [performance-benchmarker](agents/testing/performance-benchmarker.md) | パフォーマンスベンチマークと最適化。ボトルネック特定 |
| [test-results-analyzer](agents/testing/test-results-analyzer.md) | テスト結果の分析。カバレッジ分析、失敗原因調査 |
| [tool-evaluator](agents/testing/tool-evaluator.md) | ツール・ライブラリの評価。比較検討、導入判断、PoC実施 |
| [workflow-optimizer](agents/testing/workflow-optimizer.md) | 開発ワークフローの最適化。ビルド時間短縮、自動化による効率化 |
