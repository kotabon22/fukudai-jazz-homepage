# 🎷 福井大学ジャズ研究会 — ホームページ

**技術スタック**
- **公開**: Netlify（無料）
- **CMS**: Decap CMS（ブラウザだけで記事投稿）
- **画像**: Cloudinary（gitに画像を入れない）
- **ビルド**: 不要（静的HTMLをそのまま配信）

---

## 🚀 初期セットアップ（一度だけ）

### Step 1 — Cloudinary アカウント作成

1. https://cloudinary.com にアクセス → 無料登録
2. ダッシュボードの **Cloud name** と **API Key** をメモ

### Step 2 — GitHubリポジトリ作成

1. https://github.com → New repository
2. 名前例: `fukudai-jazz` → **Public** で作成
3. このフォルダの中身を全部アップロード

```bash
git init
git remote add origin https://github.com/YOUR_NAME/fukudai-jazz.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

### Step 3 — Netlify でデプロイ

1. https://netlify.com → **Add new site → Import from Git**
2. GitHub を選択 → リポジトリを選択
3. Build command: **空欄のまま**
4. Publish directory: **`.`** (ドット1つ)
5. **Deploy** → 数秒でURLが発行される

### Step 4 — Netlify Identity を有効化

1. サイトの **Site settings → Identity → Enable Identity**
2. **Registration → Invite only** に変更（外部から勝手に登録されないように）
3. **Git Gateway → Enable Git Gateway**

### Step 5 — Cloudinary を Decap CMS に設定

`admin/config.yml` を開いて以下を書き換える：

```yaml
media_library:
  name: cloudinary
  config:
    cloud_name: YOUR_CLOUD_NAME   # ← Cloudinaryのcloud nameに変える
    api_key: YOUR_API_KEY         # ← Cloudinaryのapi keyに変える
```

さらに Netlify の環境変数に API Secret を追加:
- Site settings → Environment variables
- Key: `CLOUDINARY_API_SECRET`
- Value: Cloudinary ダッシュボードの API Secret

### Step 6 — 部員を招待

1. Netlify → Identity → **Invite users**
2. 部員のメールアドレスを入力 → 招待メールが届く
3. 部員は `https://YOUR_SITE.netlify.app/admin` にアクセスしてログイン

---

## ✏️ 部員向け：記事の投稿方法

1. `https://YOUR_SITE.netlify.app/admin` にアクセス
2. Netlifyアカウントでログイン
3. **「活動報告」→「新規」** をクリック
4. タイトル・本文（Markdown）・写真（Cloudinaryにアップロード）を入力
5. **ギャラリー**に写真を最大10枚追加できる
6. **「公開」** を押すと自動的にサイトに反映

---

## 📁 ファイル構成

```
fukudai-jazz/
├── index.html          ← メインページ（編集不要）
├── netlify.toml        ← Netlify設定
├── _redirects          ← リダイレクト設定
├── admin/
│   ├── index.html      ← Decap CMS本体（編集不要）
│   └── config.yml      ← CMS設定（★ここだけ書き換える）
├── _posts/
│   ├── manifest.json   ← 記事一覧（CMSが自動更新）
│   └── *.md            ← 記事ファイル（CMSが自動生成）
├── _album/
│   ├── manifest.json   ← アルバム一覧
│   └── *.md            ← アルバムファイル
└── _data/
    ├── general.json    ← サークル基本情報
    ├── members.json    ← メンバー一覧
    ├── schedule.json   ← 活動スケジュール
    ├── links.json      ← リンクツリー
    └── sections.json   ← セクション表示設定
```

---

## 🔧 よくある問題

| 症状 | 対処 |
|------|------|
| CMSにログインできない | Netlify Identity が有効か確認 |
| 画像がアップロードできない | Cloudinaryの設定を確認 |
| 記事が反映されない | GitHubへのpushを確認（Netlifyログ参照） |
| `manifest.json` に記事が出ない | CMSで保存後、GitHubに自動pushされるまで少し待つ |

---

## 💡 引き継ぎのポイント

- **GitHubアカウントは不要**（部員はNetlify Identityだけ）
- CMSの操作はブラウザだけで完結
- 写真はCloudinaryに保存されるのでgitが重くならない
- `admin/config.yml` の設定さえ合っていれば誰でも投稿できる
