# 🎷 福井大学ジャズ研究会 — ホームページ

**完全無料スタック**
- **ホスティング**: GitHub Pages（無料）
- **CMS**: Decap CMS（無料、オープンソース）
- **画像管理**: Cloudinary（25GB/月まで無料）
- **バージョン管理**: GitHub（無料）

---

## 🚀 初期セットアップ

### Step 1 — Cloudinary アカウント作成

1. https://cloudinary.com → 無料登録
2. **Account → Details** で **Cloud name** をメモ
3. **Account → API Keys** で **API Key** をメモ

### Step 2 — GitHub リポジトリ作成

1. https://github.com → **New repository**
2. 名前: `fukudai-jazz` → **Public** で作成
3. このフォルダ全体をアップロード
4. **重要**: リポジトリの説明に以下を追加：
   ```
   GitHub Pages + Decap CMS で運営されるジャズサークルのホームページ
   ```

```bash
git init
git remote add origin https://github.com/YOUR_NAME/fukudai-jazz.git
git add .
git commit -m "Initial commit: Jazz club website with Decap CMS"
git push -u origin main
```

### Step 3 — GitHub OAuth アプリを作成（CMS認証用）

1. GitHub → **Settings → Developer settings → OAuth Apps → New OAuth App**
2. 以下を入力：
   - **Application name**: `Jazz研 CMS`
   - **Homepage URL**: `https://YOUR_GITHUB_NAME.github.io/fukudai-jazz`
   - **Authorization callback URL**: `https://YOUR_GITHUB_NAME.github.io/fukudai-jazz/admin`
3. **Client ID** と **Client Secret** をメモ

### Step 4 — GitHub Pages を有効化

1. GitHub → リポジトリ → **Settings → Pages**
2. **Source** → **Deploy from a branch**
3. **Branch** → `main` / `/ (root)` を選択
4. **Save**
5. 数分後、`https://YOUR_GITHUB_NAME.github.io/fukudai-jazz` で公開される

### Step 5 — `.env.local` ファイルをローカルで作成（git に上げない）

**ファイル名**: `.env.local`

```
CLOUDINARY_CLOUD_NAME=your_actual_cloud_name
CLOUDINARY_API_KEY=your_actual_api_key
GITHUB_CLIENT_ID=your_oauth_client_id
GITHUB_CLIENT_SECRET=your_oauth_client_secret
```

⚠️ **`.env.local` は git に上げません** — `.gitignore` で除外されます

### Step 6 — CMS にログイン

1. `https://YOUR_GITHUB_NAME.github.io/fukudai-jazz/admin` にアクセス
2. **GitHub でログイン** をクリック
3. 認可画面が出る → **認可** をクリック
4. CMS に入れば成功！

---

## ✏️ 部員向け：投稿方法

### ログイン

```
https://YOUR_GITHUB_NAME.github.io/fukudai-jazz/admin
```

**GitHub でログイン** をクリック

### 記事を投稿

1. **活動報告 → 新規** をクリック
2. タイトル・日付・写真を入力
3. ギャラリーに最大10枚の写真を追加
4. **保存** をクリック → 自動的に GitHub に push → サイトに反映 ✅

### メンバー・スケジュール・リンクを編集

**サイト設定** タブから以下を編集：
- **基本情報** — サークル名、年数など
- **メンバー** — メンバー一覧
- **活動スケジュール** — 練習日時
- **リンクツリー** — Instagram・Twitter など
- **セクション順序** — 表示順序や非表示設定

---

## 📁 ファイル構成

```
fukudai-jazz/
├── .env.local              ← OAuth・Cloudinary設定（git に上げない）
├── .env.example            ← テンプレート
├── .gitignore              ← git 除外設定
├── index.html              ← メインページ
├── _config.yml             ← Jekyll 設定（GitHub Pages 用）
├── admin/
│   ├── index.html          ← CMS 画面
│   └── config.yml          ← CMS 設定
├── _posts/                 ← 記事（CMSが自動生成）
├── _album/                 ← アルバム（CMSが自動生成）
└── _data/                  ← サイト設定（JSON）
    ├── general.json
    ├── members.json
    ├── schedule.json
    ├── links.json
    └── sections.json
```

---

## 🔐 セキュリティ

✅ **正しい方法：**
- API key・OAuth Secret は `.env.local` で管理（git に上げない）
- `.gitignore` で `.env.local` を除外
- GitHub OAuth で部員のアクセスを制御

❌ **危ない方法：**
- API key をソースコードに直接書く
- `.env.local` を git に上げる

---

## 💡 GitHub Pages vs Netlify

| 項目 | GitHub Pages | Netlify |
|------|-------------|---------|
| 無料 | ✅ 完全無料 | ✅ 無料（制限あり） |
| ビルド | Jekyll 自動 | 環境変数対応 |
| 帯域 | 制限なし | 100GB/月 |
| Decap CMS | ✅ 対応 | ✅ 推奨 |
| 初期設定 | OAuth 必須 | Identity 簡単 |

**GitHub Pages を選んだ理由：**
- ✅ 帯域制限がない
- ✅ 完全無料
- ✅ GitHub との一体化

---

## 🆘 トラブルシューティング

| 問題 | 解決方法 |
|------|---------|
| CMS にログインできない | GitHub OAuth 設定を確認 |
| 記事が公開されない | GitHub リポジトリを確認（push されてるか） |
| 写真がアップロードできない | Cloudinary API Key が正しいか確認 |
| サイトが更新されない | GitHub Pages のビルドログを確認 |

詳しくは **TROUBLESHOOTING.md** を参照

---

## 📊 デプロイの流れ

```
CMS で記事を保存
↓
Decap CMS が GitHub に commit & push
↓
GitHub Pages が自動的にビルド
↓
サイトが更新される ✅
```

（自動で全部やってくれます）

---

## 📞 参考資料

- **GitHub Pages**: https://pages.github.com/
- **Decap CMS**: https://decapcms.org/
- **Cloudinary**: https://cloudinary.com/documentation
- **GitHub OAuth**: https://docs.github.com/en/developers/apps/building-oauth-apps

---

## ✨ 次のステップ

1. ✅ Cloudinary アカウント作成 → Cloud name / API key をメモ
2. ✅ GitHub リポジトリ作成 → このフォルダを push
3. ✅ GitHub Pages を有効化
4. ✅ GitHub OAuth アプリを作成 → Client ID / Secret をメモ
5. ✅ `.env.local` を作成 → 全部の値を入力
6. ✅ `/admin` でログイン → 完了！🎉

