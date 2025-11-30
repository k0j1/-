
# 割烹食堂かいね (Kappo Shokudo Kaine) Website

福島県郡山市菜根にある「割烹食堂かいね」の公式ウェブサイトプロジェクトです。
React, TypeScript, Tailwind CSS, Vite を使用して構築されています。

## プロジェクトのセットアップ

### 1. 依存関係のインストール
プロジェクトのフォルダで以下のコマンドを実行してください。

```bash
npm install
```

### 2. 環境変数の設定 (ローカル開発用)
ローカルで開発する場合は、`.env` ファイルをプロジェクトルートに作成し、以下のAPIキーを設定してください。

```env
# Google AI Studio (AIコンシェルジュ用)
VITE_API_KEY=your_gemini_api_key_here

# Google Cloud Platform (店舗写真取得用)
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key_here
```

### 3. 開発サーバーの起動（プレビュー）
手元のブラウザで確認するには以下のコマンドを実行します。

```bash
npm run dev
```

## 画像ファイルの配置について
駐車場の画像などは `public/image/` フォルダに配置してください。
例: `public/image/Parking.png`

## GitHub Pagesへの公開方法 (本番環境)

このプロジェクトは **GitHub Actions** を使用して自動的に公開されます。
本番環境でAPIキーを有効にするには、GitHub上で「Secrets」の設定が必要です。

### APIキーの設定手順 (GitHub Secrets)
1. GitHubリポジトリの **[Settings]** タブを開きます。
2. 左メニューから **[Secrets and variables]** > **[Actions]** を選択します。
3. **[New repository secret]** をクリックし、以下の2つを登録してください。

| Name | Value (Secret) |
| :--- | :--- |
| `VITE_API_KEY` | Gemini APIキー |
| `VITE_GOOGLE_MAPS_API_KEY` | Google Maps APIキー |

### デプロイの手順
設定完了後、変更をプッシュすると自動的にデプロイされます。

```bash
git add .
git commit -m "Update site"
git push origin main
```

## トラブルシューティング

### Q. 「Google Maps API Key is missing」と表示される
GitHub上でこのエラーが出る場合、Secretsを設定しただけではまだ反映されていません。
Viteはビルド時に環境変数を埋め込むため、**Secrets設定後に必ず再デプロイ（何らかのコミットをプッシュ）** する必要があります。

**対処法:**
1. Secretsに `VITE_GOOGLE_MAPS_API_KEY` が正しく保存されているか確認する。
2. 適当な修正（READMEの空白変更など）を行い、コミット＆プッシュしてGitHub Actionsを再実行させる。

### Q. Google Maps API エラー: ApiNotActivatedMapError
ブラウザのコンソールに `ApiNotActivatedMapError` が表示される場合、APIキーに紐づくGoogle Cloudプロジェクトで **「Maps JavaScript API」** が有効になっていません。

**解決手順:**
1. [Google Cloud Console](https://console.cloud.google.com/) にアクセスします。
2. 「APIとサービス」 > 「ライブラリ」を選択します。
3. **「Maps JavaScript API」** を検索し、「有効にする」をクリックします。
4. 同様に **「Places API」** も有効にしてください。

## 構成技術
- **Framework:** React + Vite
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **AI:** Google Gemini API
- **Map:** Google Maps Places API