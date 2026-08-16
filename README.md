# StartStep 公式ウェブサイト

日本の個人事業「STARTSTEP」の公式サイトです。静的HTML/CSS/JS（ビルド不要）で構成されており、
Cloudflare Pages にそのままデプロイできます。

## 1. プロジェクト概要

- **屋号**：StartStep（スタートステップ）
- **代表者**：鈴木葉月
- **事業形態**：個人事業主
- **所在地**：東京都日野市
- **開業**：2026年6月
- **メール**：info@startstep-biz.com
- **サイト目的**：一般的な企業紹介であると同時に、Google Play・AdMob・
  D-U-N-S Number 等の審査担当者が「実在する事業者が説明通りのプロダクトを
  提供しているか」を確認するための審査対応ページを兼ねる。情報の正確性・
  事業者としての信頼性を重視した設計にしている。

## 2. デザインコンセプト

- ミニマル・洗練、信頼感・プロフェッショナルなトーン
- ペールブルー×白を基調にしたグラスモーフィズム（半透明・ぼかし）
- 柔らかい陽光のようなアンビエントライト演出（控えめ・非アニメーション主張型）
- 余白を十分に取った、装飾を絞った引き算のデザイン
- 和文フォントはシステムフォント優先（外部Webフォント読み込みなし、軽量）
- PC・スマートフォンの両方に対応したレスポンシブレイアウト

## 3. 完成した機能・ページ構成

### トップページ（`/index.html` → `/`）
以下の順でセクションを実装（アンカーリンクによるナビゲーション付き）：
1. ヒーローセクション（`#hero`）
2. なぜStartStepなのか（`#why`）
3. 私たちについて（`#about`）― ミッション／ビジョン／価値観カード
4. プロダクト（`#products`）― Studious Log 詳細 ＋ QuestLog / Studious Life（Coming Soon）
5. 事業内容（`#services`）― プロダクト開発／学習支援プロダクトの研究の2項目のみ
6. 事業概要（`#business`）― 事業者情報テーブル ＋ 現在の事業リスト
7. お問い合わせ（`#contact`）― mailtoボタン
8. フッター（プライバシーポリシー／利用規約リンク、コピーライト）

指定文言はすべて改変せずそのまま掲載。Google Playストアへのリンクや
「開発中」バッジ、「広告や課金はありません」等の実態と異なる記述は含めていません。

### 利用規約ページ（`/terms.html` → `/terms`）
指定テキストをそのまま掲載（既知の矛盾＝実際のStudious Logには広告・有料プランが
存在する点は、ユーザー指示に基づき意図的にそのまま反映。将来的な内容更新は
事業者側で別途対応予定）。

### プライバシーポリシーページ（`/privacy.html` → `/privacy`）
指定テキストをそのまま掲載（同様に既知の矛盾を含む内容をそのまま反映）。

いずれのページにも「← ホームへ」のリンクを設置し、トップページと同一の
デザイントーン（ペールブルー・グラスモーフィズム）を適用しています。

## 4. URL構成

| パス | 内容 | 備考 |
|---|---|---|
| `/` | トップページ | `index.html` |
| `/terms` | 利用規約 | `terms.html` を `_redirects` で 200 リライト |
| `/privacy` | プライバシーポリシー | `privacy.html` を `_redirects` で 200 リライト |
| `/app-ads.txt` | AdMob用 ads.txt | `text/plain` 配信（`_headers`で明示指定） |
| `/robots.txt` | クローラー制御 | `text/plain` 配信 |
| `/sitemap.xml` | サイトマップ | `application/xml` 配信 |

### Cloudflare Pages 向けの重要ファイル
- **`_redirects`**：`/terms`・`/privacy`（拡張子なしURL）を、それぞれ
  `terms.html`・`privacy.html` に **200（リライト）** で対応させています。
  既存アプリ（Studious Log）がこれらのURLを直接参照しているため、
  URLは変更していません。
- **`_headers`**：`app-ads.txt`・`robots.txt`・`sitemap.xml` が
  誤ってHTMLとして配信されないよう、`Content-Type` を明示的に指定しています
  （過去に別ツールで `app-ads.txt` がHTMLページに上書き配信された事故があったため、
  特に注意して設定しています）。

## 5. ファイル構成

```
index.html              トップページ
terms.html               利用規約（/termsとして配信）
privacy.html             プライバシーポリシー（/privacyとして配信）
app-ads.txt               AdMob審査用（text/plain）
robots.txt                クローラー制御
sitemap.xml               サイトマップ
_redirects                Cloudflare Pages 用リライトルール
_headers                  Cloudflare Pages 用 Content-Type 指定
css/
  └── style.css           全ページ共通スタイル（グラスモーフィズム／レスポンシブ）
js/
  └── main.js              モバイルナビゲーション開閉・スクロールフェードイン
images/
  ├── logo-s.png           ロゴマーク（S字モノグラム、favicon兼用）
  └── ogp.jpg               OGPシェア画像
README.md
```

## 6. データ・ストレージ

- 本サイトはテーブルAPI・データベースを一切使用しない、完全な静的サイトです。
- お問い合わせは `mailto:info@startstep-biz.com` リンクのみ（フォーム送信機能なし）。

## 7. 実装していない機能・既知の制限

- お問い合わせフォーム（メール送信フォーム）は実装していません。現状は
  mailtoリンクのみです。フォームが必要な場合は、外部フォームサービス
  （Googleフォーム等）や、CORS対応済みの外部APIとの連携をご検討ください。
- 利用規約・プライバシーポリシーの本文は、ユーザー指示に基づき「実際の
  Studious Logの実態（広告・有料プランあり）と矛盾する古い内容」を
  そのまま掲載しています。事業者側で内容更新のタイミングを検討し、
  実態に即した内容に改訂することを推奨します。
- Google Playストアへのリンクは、クローズドテスト中のため意図的に
  未掲載としています。一般公開後に追加を検討してください。

## 8. 次の開発ステップ（推奨）

1. Studious Logの一般公開後、事業概要セクションへのストアリンク追加を検討
2. 利用規約・プライバシーポリシーの内容を、実際の広告・課金仕様に合わせて改訂
3. お問い合わせフォームが必要な場合は、外部サービス連携を検討
4. 独自ドメイン（startstep-biz.com）をCloudflare Pagesに接続し、
   `app-ads.txt` が `text/plain` で配信されることを本番環境でも確認

## 9. デプロイ方法

Cloudflare Pagesへの本番デプロイは、**Publishタブ**から行ってください。
Publishタブでワンクリック公開が可能で、公開後のURLも確認できます。

独自ドメイン接続後は、以下を必ず確認してください：
- `https://startstep-biz.com/app-ads.txt` が `text/plain` として正しく表示される
- `https://startstep-biz.com/terms`・`https://startstep-biz.com/privacy` が
  それぞれ正しいページを表示する
