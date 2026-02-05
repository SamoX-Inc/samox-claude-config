---
name: notion-plan
description: Notionページのタスク内容を読み取り、開発方針設計書（Logic Design Brief）を生成してNotionページに追記するスキル。ユーザーが「/notion-plan [Notion URL]」と入力した時や、Notionのタスクから実装計画を作成したい時に使用する。
---

# Notion Plan

## 概要

このスキルはNotionページに記載されたタスク内容を分析し、構造化された開発方針設計書を自動生成してNotionページに追記します。

## ワークフロー

### 1. Notion URLの受け取り

ユーザーから以下の形式でNotion URLを受け取る:
```
/notion-plan https://www.notion.so/your-page-url
```

### 2. Notionページの内容取得

**必須:** 最初にNotion MCPツールをロードする必要があります。

```
ToolSearch with query: "+notion fetch"
```

ツールがロードされたら、`mcp__notion__notion-fetch` を使用してページ内容を取得する。

### 3. 開発方針設計書の生成

取得したタスク内容を分析し、`references/template.md` に基づいて以下の構造で設計書を生成する:

**重要な制約:**
- 具体的なファイル名やコードの実装詳細は書かない
- 「データモデルの変更」「ビジネスロジック（ルール）」「画面遷移と役割」にフォーカス
- レビューワーが「仕様の矛盾」や「考慮漏れ」に気づきやすい簡潔な記述

**テンプレート構造:**

詳細なテンプレートは `references/template.md` を参照してください。基本構造は以下の通り:

1. 概要と目的
   - 実装内容
   - 目的/Why

2. バックエンド方針（データとルール）
   - データモデル (DB)
   - API & ロジック

3. フロントエンド方針（画面と遷移）
   - 画面構成

### 4. Notionページへの追記

生成した設計書を `mcp__notion__notion-update-page` を使用してNotionページに追記する。

**追記時の注意:**
- 既存のコンテンツを上書きしないこと
- ページの末尾に新しいセクションとして追加すること
- 見出しレベルを適切に設定すること

## 使用例

```
/notion-plan https://www.notion.so/abc123/Task-XYZ
```

このコマンドを実行すると:
1. 指定されたNotionページを取得
2. タスク内容を分析
3. 開発方針設計書を生成
4. Notionページに追記

## リソース

### references/

- `template.md`: 開発方針設計書の詳細なテンプレート。設計書生成時に必ず参照すること。
