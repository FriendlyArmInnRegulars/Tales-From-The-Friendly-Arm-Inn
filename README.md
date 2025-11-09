# Tales From The Friendly Arm Inn

EET（Enhanced Edition Trilogy）、IWD1-EET、IWD2-EET Modの包括的な攻略ガイドサイト

## 概要

このプロジェクトは、Baldur's Gate用のEET Modシリーズのための情報サイトです。以下の内容を提供します：

- **クエストガイド**: すべてのクエストの詳細な攻略情報
- **アイテムデータベース**: 武器、防具、アイテムの完全なデータベース
- **NPC情報**: 仲間NPCと重要キャラクターの詳細
- **敵データベース**: ボスと敵の攻略法
- **魔法ガイド**: すべての魔法の詳細情報

## 技術スタック

- **静的サイトジェネレーター**: Jekyll 4.3
- **ホスティング**: GitHub Pages
- **言語**: 日本語・英語（多言語対応）
- **データ管理**: JSON + Markdown

## ローカル開発

### 前提条件

- Ruby 3.1以上
- Bundler

### セットアップ

```bash
# 依存関係のインストール
bundle install

# ローカルサーバーの起動
bundle exec jekyll serve

# ブラウザで http://localhost:4000 を開く
```

### ビルド

```bash
# 本番環境用ビルド
JEKYLL_ENV=production bundle exec jekyll build
```

## ディレクトリ構造

```
/
├── _config.yml           # Jekyll設定
├── _data/               # JSONデータファイル
│   ├── weapons.json
│   ├── armor.json
│   ├── items.json
│   ├── npcs.json
│   ├── enemies.json
│   └── spells.json
├── _layouts/            # ページレイアウト
├── _includes/           # 再利用可能なコンポーネント
├── _quests/            # クエストコンテンツ（Markdown）
├── assets/             # CSS, JS, 画像
├── database/           # データベースページ
└── index.html          # トップページ
```

## コンテンツの追加

### クエストの追加

`_quests/` ディレクトリに新しいMarkdownファイルを作成：

```markdown
---
layout: quest
title: "クエスト名"
mod: EET
type: メインクエスト
level: 3-5
lang: ja
rewards:
  - "経験値: 1000XP"
  - "報酬金: 500ゴールド"
---

クエストの内容...
```

### アイテムの追加

`_data/weapons.json`（または他のJSONファイル）にデータを追加：

```json
{
  "id": "item_id",
  "name": {
    "ja": "日本語名",
    "en": "English Name"
  },
  "type": "longsword",
  "description": {
    "ja": "説明",
    "en": "Description"
  }
}
```

## デプロイ

このサイトはGitHub Actionsを使用して自動的にデプロイされます。`main`ブランチにプッシュすると、自動的にビルドされてGitHub Pagesに公開されます。

### GitHub Pagesの設定

1. リポジトリの Settings > Pages に移動
2. Source を "GitHub Actions" に設定
3. `main`ブランチにプッシュすると自動デプロイ

## ライセンス

このプロジェクトは非公式ファンサイトです。Baldur's GateはBeamdog社とWizards of the Coast社の登録商標です。

## 貢献

貢献を歓迎します！プルリクエストを送信してください。
