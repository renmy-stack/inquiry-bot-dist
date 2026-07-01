# inquiry-bot — 配布

新規の問い合わせ（RedMineチケット）に対し、過去のQ&A（Excel／DMSF）から
**類似の過去問い合わせを自動抽出**し、**想定解答案のドラフト**をチケットにコメント投稿するツールの配布用リポジトリです。
最終判断は人間が行う「半自動」運用。

> このリポジトリは **exe の配布専用** です。ソースコードは非公開リポジトリで管理しています。

## ダウンロード

最新版はこちら 👉 **[Releases](../../releases/latest)** から `inquiry-bot-vX.Y.Z.zip` をダウンロード

- Windows 64bit / **インストール不要（Python も不要）**
- zipを展開し、フォルダ内で使用

## 使い方（Python不要・GUIで完結）

zip を展開すると次が入っています。

```
inquiry-bot/
├── inquiry-bot-gui.exe    GUI（設定＆実行／これだけ使えばOK）
├── inquiry-bot.exe        CLI（自動化・スクリプト用）
├── config.example.json    設定テンプレート（GUIを使うなら不要）
├── qa-template.xlsx       Q&A Excel の雛形（スキーマ＋記入例）
└── はじめに.txt           かんたん手順
```

### かんたん3ステップ（GUI）

1. **`inquiry-bot-gui.exe` をダブルクリック**
2. **「設定」タブ**で入力して「💾 設定を保存」
   - RedMine URL ／ APIアクセスキー ／ プロジェクト識別子
   - Q&Aの場所：`RedMine DMSF`（ファイルID）か `ローカルExcel`（`qa.xlsx`）を選ぶ
3. **「実行」タブ**でチケット番号を入れて「▶ 実行」
   - まずは「投稿せず確認のみ」にチェックして内容確認 → 外して実投稿
   - RedMineの該当チケットに 🤖 の解答案コメントが付く → 人が妥当性を判断

> config.json はGUIが自動生成するので、**JSONの手編集は不要**です。

### CLI（自動化したい場合）

`config.json` を用意し（GUIで保存 or `config.example.json` をコピー編集）：
```
inquiry-bot.exe <チケット番号>          解答案をチケットにコメント投稿
inquiry-bot.exe <チケット番号> --dry     投稿せず内容だけ表示
```

## 前提（会社側）

- RedMine：REST API 有効 ＋ APIアクセスキー発行
- Q&Aデータ：DMSFにExcelを置く（推奨）／またはローカルExcel
- （任意）問い合わせ用メールアカウント：RedMine標準のIMAP受信で自動起票すると入口も自動化

## 外部通信

- 通信先は **設定した社内RedMineのみ**（REST API）。それ以外への外部送信はありません。

## 動作環境

Windows 10 / 11（64bit）。追加のランタイム不要。
