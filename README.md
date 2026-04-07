# team-knowledge

社内ナレッジ共有ハブです。全社共通のルール・規定、Claude Code活用のベストプラクティス、おすすめスキルなどを一元管理しています。

## ナレッジの追加方法

### 方法1: Claude Codeのスキルで追加（対話型）

Claude Code上で `/add-knowledge` スキルを実行し、追加したい内容を伝えてください。
AIが既存ナレッジとの重複確認・適切な配置・PR作成まで行います。

```
> /add-knowledge
> リモートワーク規定が決まりました。週3日まで、事前申請必須で...
```

**事前準備**: [スキルのセットアップ](#スキルのセットアップ) を参照

### 方法2: source/ にファイルを投入（自動処理）

`source/` フォルダにファイルを追加してpushすると、GitHub Actionsが自動でナレッジを整理・配置し、PRを作成します。

**GitHub Web UIから（ブラウザのみ、ツール不要）:**
1. [source/ フォルダ](../../tree/main/source) を開く
2. 「Add file」→「Create new file」
3. ファイル名と内容を入力して「Commit changes」

**ターミナルから:**
```bash
cd team-knowledge
cp 議事録.md source/
git add source/ && git commit -m "add: 議事録" && git push
```

投入後、数分でPRが作成されます。PRをレビュー・承認するとナレッジが反映されます。

## リポジトリ構成

```
company/          全社共通の規定・ルール・用語など
skills/
  approved/       承認済みの共有スキル
  proposals/      提案中のスキル（PRで承認後にapproved/へ移動）
best-practices/   Claude Code活用のTips・ベストプラクティス
teams/
  registry.md     チーム専用リポジトリへのリンク集
source/           ナレッジ投入口（自動処理用、処理後にファイルは削除されます）
```

## チーム専用リポジトリについて

GitHubの仕様上、リポジトリ内のフォルダ単位で読み取り権限を分けることはできません。
他チームに見せたくない情報（戦略、顧客情報など）は、チーム専用リポジトリで管理してください。

各チームのリポジトリは [teams/registry.md](teams/registry.md) にリンクがあります。

## 承認フロー

このリポジトリでは [CODEOWNERS](CODEOWNERS) とブランチ保護により、ナレッジの追加・変更にはレビュー承認が必要です。

- 誰でもPR（変更提案）を出せます
- マージには CODEOWNERS に指定された承認者のapproveが必要です
- `source/` からの自動処理もPR経由なので、同じ承認フローが適用されます

## セットアップ

### スキルのセットアップ

`/add-knowledge` スキルを使うには、以下のファイルを作成してください:

```
~/.claude/skills/add-knowledge/SKILL.md
```

スキルファイルの内容は管理者から共有されます。

### GitHub CLIの認証（ターミナルから使う場合）

```bash
gh auth login
```

## ファイルの書き方

- Markdown形式で記述してください
- ファイル名は英語のkebab-case（例: `deployment-rules.md`）
- 各ファイルの先頭に概要を1行書いてください
- 1ファイルが大きくなりすぎた場合はトピック単位で分割します
