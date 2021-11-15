# コーディングガイドライン & 命名規則

## フロントエンドガイドライン

### HTML

#### HTMLマークアップの仕様書

* [WHATWG](https://whatwg.org/)のHTML Standard(英文): <https://html.spec.whatwg.org/>
  * HTML5という呼称自体は2021年1月に廃止され、HTML Standardが標準仕様に - HTML5.2とHTML Living standardの違い: <https://www.modis.jp/staffing/insight/column_122/>
* HTML Standard(HTML Living Standard)の日本語訳(部分訳)はこちら: <https://github.com/whatwg/html/wiki/Translations>

#### マークアップチェッカー / バリデーター

* HTML Conformance Checkers ※2021年時点有効と判断: <https://whatwg.org/validator/> = <https://validator.w3.org/nu/>
* HTMLHintを利用: <https://htmlhint.com/>
  * lint設定内容: <https://github.com/ishimasar/pattern-library/blob/master/.htmlhintrc>
* VScodeエディタ拡張機能「[W3C Validation](https://marketplace.visualstudio.com/items?itemName=Umoxfo.vscode-w3cvalidation)」によるバリデーションも利用OK。(ただしJREが必要、たまに動かなくなるなど少し面倒)

#### Web(HTML)テンプレートエンジンの使用有無

* Web(HTML)テンプレートエンジンは積極的・能動的に使用しない。素のHTMLが結局扱いやすく、見通しやすいため
* Webアプリケーションフレームワークやライブラリ上で機構として組み込まれたものや、ファイル構成上の利点が多い場合はこの限りではない
  * 例
    * Node.js(/Express)アプリケーションにおける[EJS](https://ejs.co/)
    * Ruby on RailsにおけるERB、PHP系フレームワークにおける[Twig](https://twig.symfony.com/)
    * ほかには[Handlebars](https://handlebarsjs.com/)、[Nunjucks](https://mozilla.github.io/nunjucks/)
    * Pug、Blade、Slim、Smarty、Edge.jsは個人的には選択しません

### CSS

#### プリプロセッサ言語Sass(サス、サース)を活用

* 基本的にSCSS構文(拡張子: .scss)を選択

### JavaScript

* eslint

### メディア (画像・音声・動画など)

### フォント

#### web fontの使用

* 和文web fontはファイルサイズが重いため、基本的に使用を避ける

### アクセシビリティ

### パフォーマンス

### ビルドツールとバージョン管理

### OS / ブラウザサポート・最適化

### その他

#### 提供言語 (ローカリゼーション)

#### Deployment / Integration

---

### 命名規則

### 命名の考え方・原則

#### Semantic (意味型)とDeclarative (宣言型)

### ファイル命名

#### コードファイル

#### メディアファイル

### CSSセレクタ命名 (class、id)ほか

#### ECSS + RSCSSを採用

#### Scoped CSSまたはCSS Modulesの場合

#### name属性

#### data-\*属性

#### class命名サンプル集

### JavaScriptにおける命名

#### 関数、変数、メソッド、名前空間

#### classオブジェクト、列挙型

---

## 知っておきたいWeb・ソフトウェア開発デザインおよびバックエンドの知識

### システム設計 / 要件定義

### データべース設計

#### ER図

#### MySQL / PostgreSQL

### UML (統一モデリング言語 / Unified Modeling Language)

#### シーケンス図

#### オブジェクト図

#### ユースケース図

#### クラス図

### オブジェクト指向

### サーバー知識

### コマンドライン (CLI / CUI)

### セキュリティ

### WordPressおよびPHP

### Ruby on Rails

### Python

---

## 制作・運営

石井 将直 / Masanao Ishii (Cloudy knot)
