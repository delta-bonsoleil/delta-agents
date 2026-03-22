# delta-agents

deltaシステムで採用するエージェント定義の原本リポジトリ。

## 構造

部署（役割領域）ごとにディレクトリを分け、各エージェント定義を配置する。

```
agents/
├── design/              # デザイン
├── engineering/         # エンジニアリング
├── marketing/           # マーケティング
├── operations/          # オペレーション
├── planning/            # 企画立案（ブレスト・リサーチ・提案）
├── product/             # プロダクト
├── project-management/  # プロジェクト管理
├── security/            # セキュリティ・監査
└── testing/             # テスト・QA
```

`agents/` ディレクトリをそのまま `~/.claude/agents/` にコピーして使える。

## エージェント定義フォーマット

各エージェントは `.md` ファイルで定義する。

```markdown
---
name: エージェント名
description: 一行の説明
tools: 使用可能なツール（カンマ区切り）
model: 使用モデル
---

（エージェントのプロンプト本文）
```

## エージェント一覧

| 部署 | 名前 | 説明 |
|------|------|------|
| security | [mephi](agents/security/mephi.md) | CCO/セキュリティ監査役 悪魔駆動開発(DDD)提唱者 |
