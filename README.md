# SamoX Claude Skills

Claude Code用のカスタムスキル集です。

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

詳細は [notion-plan/SKILL.md](./notion-plan/SKILL.md) を参照してください。

## インストール方法

### 前提条件

- Claude Code CLIがインストールされていること
- Notion MCP serverが設定されていること（notion-planを使用する場合）

### インストール手順

1. このリポジトリを任意の場所にクローンします:

```bash
cd ~/projects  # または任意のディレクトリ
git clone https://github.com/SamoX-Inc/samox-claude-skills.git
```

2. 使いたいスキルへのシンボリックリンクを作成します:

```bash
# notion-planをインストールする場合
ln -s ~/projects/samox-claude-skills/notion-plan ~/.claude/skills/notion-plan
```

3. Claude Codeを再起動するか、新しいセッションを開始します。

4. `/notion-plan` コマンドで使用できるようになります。

## スキルのアンインストール

シンボリックリンクを削除するだけです:

```bash
rm ~/.claude/skills/notion-plan
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
