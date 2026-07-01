# inquiry-bot — 配布

新規の問い合わせ（RedMineチケット）に対し、過去のQ&A（Excel／DMSF）から
**類似の過去問い合わせを自動抽出**し、**想定解答案のドラフト**をチケットにコメント投稿するツールの配布用リポジトリです。
最終判断は人間が行う「半自動」運用。

> このリポジトリは **exe の配布専用** です。ソースコードは非公開リポジトリで管理しています。

## ダウンロード

最新版はこちら 👉 **[Releases](../../releases/latest)** から `inquiry-bot-vX.Y.Z.zip` をダウンロード

- Windows 64bit / **インストール不要（Python も不要）**
- zipを展開し、フォルダ内で使用

## 使い方（Python不要）

zip を展開すると次の3点が入っています。

```
inquiry-bot/
├── inquiry-bot.exe        本体（Python同梱）
├── config.example.json    設定テンプレート（config.json にコピーして使う）
└── qa-template.xlsx       Q&A Excel の雛形（スキーマ＋記入例）
```

1. `config.example.json` を **`config.json`** にコピーし、`<...>` を実値に編集
   - `url` … 社内RedMineのURL
   - `api_key` … RedMineのAPIアクセスキー
   - `project_identifier` … 対象プロジェクト識別子
   - DMSFを使う場合: `qa_dmsf_file_id` にファイルIDを設定（`qa_excel_local` は `null`）
   - DMSFを使わない場合: `qa_template.xlsx` を埋めて `qa.xlsx` として置き、`qa_excel_local` に `"qa.xlsx"`
2. コマンドプロンプトで実行:
   ```
   inquiry-bot.exe <チケット番号>          解答案をチケットにコメント投稿
   inquiry-bot.exe <チケット番号> --dry     投稿せず内容だけ表示（まず動作確認に）
   ```
3. RedMineの該当チケットに 🤖 の解答案コメントが付く → 人が妥当性を判断

## 前提（会社側）

- RedMine：REST API 有効 ＋ APIアクセスキー発行
- Q&Aデータ：DMSFにExcelを置く（推奨）／またはローカルExcel
- （任意）問い合わせ用メールアカウント：RedMine標準のIMAP受信で自動起票すると入口も自動化

## 外部通信

- 通信先は **設定した社内RedMineのみ**（REST API）。それ以外への外部送信はありません。

## 動作環境

Windows 10 / 11（64bit）。追加のランタイム不要。
