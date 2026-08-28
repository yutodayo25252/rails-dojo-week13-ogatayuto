# CodeShelf - Git 練習用 Rails アプリ

このリポジトリは、Rails アプリを題材に Git の基本操作を練習するための教材です。

主に次の流れを練習します。

- ファイルを変更する
- `git status` で状態を見る
- `git diff` で変更内容を見る
- `git add ファイル名` で commit に含める変更を選ぶ
- `git commit -m "メッセージ"` で変更を記録する
- `git log --oneline` で履歴を見る
- `git push origin main` で GitHub へ送る

## アプリについて

CodeShelf は、技術記事を投稿できる小さな Rails アプリです。

授業では、まず Markdown ファイルを変更し、そのあと Rails の画面文言や見た目を少しずつ変更して、変更ごとに commit と push を行います。

## 起動

Codespaces のターミナルで次を実行します。

```bash
bin/rails db:prepare
bin/rails server
```

ブラウザで `/` または `/articles` を開くと、記事一覧画面が表示されます。

## 注意

このリポジトリは第7週 Git 基礎演習用です。
第6週の CRUD デバッグ演習用リポジトリとは異なり、最初から正常に動く状態です。

## productionモードの確認

通常のdevelopmentモードとtest環境ではSQLite3を使用します。

AWSデプロイ授業で使用するproductionモードだけ、`DATABASE_URL`で指定したPostgreSQLへ接続します。

PostgreSQLを使ったローカル確認では、`.devcontainer/postgres/devcontainer.json`を選択してdevcontainerを起動してください。通常の`.devcontainer/devcontainer.json`にはPostgreSQLを追加していません。

Dev Container CLIを使う場合は、このリポジトリのルートディレクトリで次を実行します。

```bash
devcontainer up \
  --workspace-folder . \
  --config .devcontainer/postgres/devcontainer.json
```

PostgreSQL用devcontainer内では、次のコマンドでproduction環境を準備できます。

このdevcontainerではPostgreSQL 18を起動し、接続先を`POSTGRES_DATABASE_URL`へ設定します。通常のdevelopmentモードには適用されず、productionモードだけがこの値を使用します。AWSでは`DATABASE_URL`を使用します。

```bash
export RAILS_ENV=production
export SECRET_KEY_BASE="$(bin/rails secret)"
bin/rails db:prepare
bin/rails server -b 0.0.0.0 -p 3000
```
