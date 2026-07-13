# StartStep 公式サイト

StartStep（日本の個人事業主）の公式ウェブサイトです。D-U-N-S Number の登録審査、
Apple Developer（Organization）、Google Play（Organization）、および学習記録アプリ
**Studious Log** の紹介を目的としています。日本語を主言語とした静的サイトです。

## 技術構成

- 静的 HTML5 ― **ビルド不要・Node.js 不要**
- Tailwind CSS（CDN）
- 最小限のバニラ JavaScript（著作年の更新・スクロール表示）
- 画像なし ― SVG アイコンのみ
- レスポンシブ対応、SEO / OGP / Twitter Card / favicon 対応

## ファイル構成

```
/
├── index.html      # トップ：ヒーロー / なぜStartStep / 私たちについて / プロダクト / サービス / 事業概要 / お問い合わせ
├── favicon.svg     # ミニマルな「S」マーク
├── robots.txt
├── sitemap.xml
├── privacy.html    # プライバシーポリシー（Studious Log バージョン1）
├── terms.html      # 利用規約（Studious Log バージョン1）
└── README.md
```

## Cloudflare Pages へのデプロイ

1. このフォルダを GitHub リポジトリへ push します。
2. Cloudflare ダッシュボード：**Workers & Pages → Create → Pages → Connect to Git**。
3. リポジトリを選択します。
4. ビルド設定：
   - **Framework preset:** `None`
   - **Build command:** *(空欄)*
   - **Build output directory:** `/`
5. デプロイ。Cloudflare が静的ファイルをそのまま配信します。

### 独自ドメイン

Pages プロジェクトの **Custom domains** で `startstep-biz.com` を追加し、DNS の案内に
従って設定します。公開後、canonical URL・`robots.txt`・`sitemap.xml` はすべて
`https://startstep-biz.com/` を指すようになっています。

## 公開前に記入する項目

`index.html` の「事業概要」表に、【 … 】で記した記入予定の項目があります。

- **代表者**（氏名）
- **所在地**
- **開業**（開業年月）

これらは D-U-N-S / Apple / Google の審査で確認される項目です。公開前に、必ず実際の
情報へ置き換えてください。

## お問い合わせ

info@startstep-biz.com
