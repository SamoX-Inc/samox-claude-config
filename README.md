# SamoX Claude Config

Claude Code用のカスタムスキル、エージェント、設定ファイルのリポジトリです。

## スキル一覧

### notion-plan

Notionページのタスク内容を読み取り、開発方針設計書（Logic Design Brief）を生成してNotionページに追記するスキルです。

**機能:**
- Notionページの内容を取得
- タスク内容を分析して構造化された設計書を自動生成
- 生成した設計書をNotionページに追記

**使用例:**
```
/notion-plan https://www.notion.so/your-page-url
```

詳細は [notion-plan/SKILL.md](./skills/notion-plan/SKILL.md) を参照してください。

## エージェント一覧

### notion-task-implementer

会話フロー設計書に基づいて機能を実装し、コミットを作成し、NotionタスクIDをプレフィックスとしたPRをdevブランチに作成するエージェントです。

**機能:**
- NotionタスクID（SX-XXX形式）を取得
- 会話フロー設計書を読み込んで実装
- タスクIDをプレフィックスとしたコミットを作成
- devブランチへのPRを作成

**使用方法:**
Task toolを使用してこのエージェントを起動し、NotionタスクIDを指定します。

詳細は [agents/notion-task-implementer.md](./agents/notion-task-implementer.md) を参照してください。

### linear-task-plan

LinearイシューのタスクIDを受け取り、タスク内容を分析して開発方針設計書（Logic Design Brief）を生成し、Linearイシューにコメントとして投稿するエージェントです。

**機能:**
- LinearタスクID（SX-XXX形式）からイシュー内容を取得
- タスク内容を分析して構造化された設計書を自動生成
- 生成した設計書をLinearイシューにコメントとして投稿

**使用方法:**
Task toolを使用してこのエージェントを起動し、LinearタスクIDを指定します。

**前提条件:**
- Linear MCP serverが設定されていること

詳細は [agents/linear-task-plan.md](./agents/linear-task-plan.md) を参照してください。

### linear-task-implementer

LinearイシューのIDを受け取り、イシューの概要とコメント（設計書を含む）を読み取って要件を理解し、実装してdevブランチへのPRを作成するエージェントです。

**機能:**
- LinearタスクID（SX-XXX形式）からイシュー内容とコメントを取得
- 開発方針設計書（コメント内）を読み取って要件を理解
- Linearが生成したgitブランチ名を使用して実装
- タスクIDをプレフィックスとしたコミット・PRを作成

**使用方法:**
Task toolを使用してこのエージェントを起動し、LinearタスクIDを指定します。

**前提条件:**
- Linear MCP serverが設定されていること

詳細は [agents/linear-task-implementer.md](./agents/linear-task-implementer.md) を参照してください。

## インストール方法

### 前提条件

- Claude Code CLIがインストールされていること
- Notion MCP serverが設定されていること（notion-planを使用する場合）
- Linear MCP serverが設定されていること（linear-task-plan, linear-task-implementerを使用する場合）

### インストール手順

1. このリポジトリを任意の場所にクローンします:

```bash
cd ~/projects  # または任意のディレクトリ
git clone https://github.com/SamoX-Inc/samox-claude-config.git
```

2. 使いたいスキルやエージェントへのシンボリックリンクを作成します:

```bash
# スキルをインストール（例: notion-plan）
ln -s ~/projects/samox-claude-config/skills/notion-plan ~/.claude/skills/notion-plan

# エージェントをインストール（例: notion-task-implementer）
ln -s ~/projects/samox-claude-config/agents/notion-task-implementer.md ~/.claude/agents/notion-task-implementer.md

# エージェントをインストール（例: linear-task-plan）
ln -s ~/projects/samox-claude-config/agents/linear-task-plan.md ~/.claude/agents/linear-task-plan.md

# エージェントをインストール（例: linear-task-implementer）
ln -s ~/projects/samox-claude-config/agents/linear-task-implementer.md ~/.claude/agents/linear-task-implementer.md
```

3. Claude Codeを再起動するか、新しいセッションを開始します。

4. スキルは `/notion-plan` コマンド、エージェントはTask toolから使用できるようになります。

## アンインストール

シンボリックリンクを削除するだけです:

```bash
# スキルのアンインストール
rm ~/.claude/skills/notion-plan

# エージェントのアンインストール
rm ~/.claude/agents/notion-task-implementer.md
```

## 開発者向け

### 新しいスキルの追加

1. このリポジトリをフォークまたはブランチを作成
2. 新しいスキル用のディレクトリを作成
3. `SKILL.md` とその他必要なファイルを追加
4. `README.md` のスキル一覧に追加
5. プルリクエストを作成

## ライセンス

MIT License

## 貢献

プルリクエストや Issue は歓迎します！
