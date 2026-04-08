# company-knowledge

社内ナレッジ共有ハブです。全社共通の規定・ルール、Claude Code活用のベストプラクティス、おすすめスキルなどを一元管理しています。

## ナレッジの追加方法

`source/` フォルダにファイルを追加してpushすると、GitHub Actionsが自動でナレッジを整理・配置し、PRを作成します。

**GitHub Web UIから（ブラウザのみ、ツール不要）:**
1. [source/ フォルダ](../../tree/main/source) を開く
2. 「Add file」→「Create new file」
3. ファイル名と内容を入力して「Commit changes」

**ターミナルから:**
```bash
cd company-knowledge
cp 議事録.md source/
git add source/ && git commit -m "add: 議事録" && git push
```

投入後、数分でPRが作成されます。PRをレビュー・承認するとナレッジが反映されます。

## リポジトリ構成

```
company/              全社共通の規定・ルール
claude/
  skills/             承認済み・提案中の共有スキル
  best-practices/     Claude Code活用のTips・ベストプラクティス
repos/
  registry.md         専用リポジトリ（チーム・プロジェクト）へのリンク集
source/               ナレッジ投入口（処理後にファイルは削除されます）
```

## 専用リポジトリについて

GitHubの仕様上、リポジトリ内のフォルダ単位で読み取り権限を分けることはできません。
他チームに見せたくない情報（戦略、顧客情報など）は、チームやプロジェクトの専用リポジトリで管理してください。

専用リポジトリの新規作成は、Claude Codeで `create-knowledge-repo` スキルを実行してください。

各専用リポジトリは [repos/registry.md](repos/registry.md) にリンクがあります。

## 承認フロー

このリポジトリでは [CODEOWNERS](CODEOWNERS) とブランチ保護により、ナレッジの追加・変更にはレビュー承認が必要です。

- 誰でもPR（変更提案）を出せます
- マージには CODEOWNERS に指定された承認者のapproveが必要です
- `source/` からの自動処理もPR経由なので、同じ承認フローが適用されます

## ファイルの書き方

- Markdown形式で記述してください
- ファイル名は英語のkebab-case（例: `deployment-rules.md`）
- 各ファイルの先頭に概要を1行書いてください
