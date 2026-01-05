# x-archive
Xが死んだ時に備えて、ローカルで自分のtweetを見れる  &amp; 高速検索できるWEBアプリ

###  仕様

Twitter(X)の公式アーカイブデータをローカル環境に永久保存し、高速検索・閲覧するためのセルフホスト型ツールです。

## 🚀 開発の背景
Twitter(X)のプラットフォームとしての不確実性やAPIの制限に左右されず、自分が過去に発信した「思考の資産」を100%手元で管理・活用するために開発しました。

## ✨ 特徴
- **完全ローカル完結**: 外部サーバーへのデータアップロードは一切不要。プライバシーを完全に保護。
- **超高速検索**: SQLiteの全文検索(FTS5)を採用し、数万件のツイートからミリ秒単位で検索可能。
- **オフライン・メディア表示**: アーカイブ内の画像・動画をローカルパスで直接参照し、当時のタイムラインを再現。
- **一撃起動**: Docker Composeにより、データの変換から閲覧環境の構築までを自動化。

## 🛠 技術スタック
- **Runtime**: [Bun](https://bun.sh/) (高速なパースとSQLite操作)
- **Database**: [SQLite](https://sqlite.org/) (ポータブルな単一ファイル構成)
- **Frontend**: [Next.js](https://nextjs.org/) (App Router, Tailwind CSS, shadcn/ui)
- **Container**: [Docker](https://www.docker.com/)

## 📦 ディレクトリ構成
```text
.
├── data/               # Twitterアーカイブの `tweets.js` と `tweet_media/` を配置
├── db/                 # 生成された `tweets.sqlite` が保存される
├── scripts/            # Bunによる変換・シードスクリプト
├── src/                # Next.js のソースコード
├── Dockerfile
└── docker-compose.yml

```

## 🛠 使い方

1. Twitterの設定から「データのアーカイブをダウンロード」をリクエストし、ZIPを入手。
2. 本リポジトリを `git clone` する。
3. `data/` ディレクトリにアーカイブ内の `tweets.js` と `tweet_media` フォルダをコピー。
4. 以下のコマンドを実行：
```bash
docker compose up

```


5. `http://localhost:3000` にアクセス。

## 📝 データベース設計 (SQLite)

### tweets テーブル

| カラム名 | 型 | 内容 |
| --- | --- | --- |
| id | TEXT (PK) | ツイートID |
| full_text | TEXT | ツイート本文 |
| created_at | TEXT | 投稿日時 |
| media_urls | TEXT | 画像/動画のローカルパス(JSON形式) |

```

---

### 3. 今後の進め方へのアドバイス

* **GitHubリポジトリの設定**: 自分のツイート内容（`tweets.js`）や生成されたDB（`tweets.sqlite`）には個人情報が含まれるため、**必ず「Privateリポジトリ」**として作成してください。
* **`.gitignore` の設定**: 
    ```text
    data/
    db/*.sqlite
    node_modules/
    .env
    ```
    これらを `.gitignore` に入れて、ソースコードだけを公開するようにしておけば、将来的に「公開用ポートフォリオ」として見せる際も安全です。

**「リポジトリ作成」の準備は整いましたね！**
まずはこの構成で `git init` して、最初の `convert.ts` （変換スクリプト）を書き始めましょうか？必要であれば、具体的なスクリプトの内容も作成できます。


