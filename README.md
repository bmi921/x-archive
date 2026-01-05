# x-archive
Xが死んだ時に備えて、ローカルで自分のtweetを見れる  &amp; 高速検索できるWEBアプリ

リポジトリ作成、素晴らしいですね！
「損得勘定」で選考にも有利に働き、かつ自分自身もずっと使える「資産」になるような名前と仕様書をまとめました。

---

### 1. リポジトリ名の案

「X（旧Twitter）」と「永久保存（Vault/Archive）」を掛け合わせた、短くて覚えやすいものがおすすめです。

* **`X-Vault`** （Xの保管庫。シンプルでかっこいい）
* **`Eternity-X`** （永遠のX。データが消えないことを強調）
* **`Tideline`** （タイムライン＋潮位線。記録が残る場所という意味の造語）
* **`X-Archive-Bun`** （技術スタックを明示した実利的な名前）

個人的には、ポートフォリオ映えもする **`X-Vault`** がイチオシです。

---

### 2. 仕様書（README.md）の構成案

そのままリポジトリの `README.md` に使える形式でまとめました。

```markdown
# X-Vault

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

```
