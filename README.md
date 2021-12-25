# コーディングガイドライン & 命名規則

## フロントエンドガイドライン

### 共通コーディング規約

#### 対象言語

* HTML
* CSS
* JavaScript
* PHP、Ruby、Python

#### 構文チェックと書き方

* 作業完了後、言語ごとのチェッカー/バリデーター/リンターなどのツールを通し、その指摘項目に従う、または参照・判断基準にする、自動修正をする(言語ごとの推奨ツールは以下に記載)
  * フレームワークやライブラリなどを導入している場合でも上記順守
* テストツール(Jest、Seleniumなど)、CI/CD(huskyなど)、テストコードの活用は問題ない
* インデントはspace2つ(半角スペース2つ)。これ以外のspace数、タブによるインデントは原則禁止。もちろん全角スペースもダメ

### HTML

#### マストチェック

* 「The Nu Html Checker」で必ずコードの構文チェックおよびできる範囲でエラー修正をする
  * <https://validator.w3.org/nu/> または <https://validator.w3.org/nu/#textarea>
  * The Nu Html Checkerは「ブックマークレットの利用」「ローカルに実行環境を構築」も可能
    * 参考：<https://a11y-guidelines.freee.co.jp/explanations/nu-html-checker.html>
* 「HTML Outliner」で必ず適切な文書構造マークアップになっているかの確認をする
  * <https://gsnedders.html5.org/outliner/>
  * Chrome拡張機能：<https://chrome.google.com/webstore/detail/html5-outliner/afoibpobokebhgfnknfndkgemglggomo>

#### 推奨チェックツール

* HTMLhint(エディタ拡張機能およびnpm module)
* W3C Validator(エディタ拡張機能)

#### 標準仕様書(基準となる参照元・出典)

* 「Living Standard」by WHATWG
  * <https://html.spec.whatwg.org/multipage/>

#### 規約

* セマンティックなマークアップを心がける
* head要素内項目(meta、OGP、link、script、解析ツール系ほか)から、できる範囲で埋めていく
  * head内マークアップ初期テンプレートは[こちら](https://raw.githubusercontent.com/ishimasar/coding-guidelines/master/docs/html-head-item-template.html)を参照・活用する
* 「HTML ガイドライン - MDN プロジェクト」の内容に則る
  * <https://developer.mozilla.org/ja/docs/MDN/Guidelines/Code_guidelines/HTML>
    * 「クラス名と ID 名」項のみ無視してOK
* link要素に`type="text/css`、script要素に`type="text/javascript"`は要素デフォルト値のため記述不要。誤りをよく見るので記載
* div、span要素の利用は必要最低限に留め、コーディング上で無意味な多重ネストは避ける。ネストしないと要件を満たせない場合はこの限りでない
  * 根拠：ネスト増加によるリーダビリティ低下およびメンテナンス性低下、バグ発生率上昇の防止
* a要素はアンカーリンク機能(ページ遷移、ページ内移動)に限定して使用する。href属性必須。そのほかの用途では使用不可
  * `<a href="javascript:void(0); ~>`は使用不可。divに置き換える
* button要素はアンカーリンク機能(ページ遷移、ページ内移動)での利用不可。submitやそのほかインタラクティブ機能で使用する
  * 根拠：a要素が担う機能のため
* a、button要素で実現できる機能をdiv、span要素等での代替禁止
  * 根拠：セマンティックではない。HTML本来の機能を消しバグ発生率が高くなる
* img要素には必ずalt属性を記述する。属性値は文脈上説明が必要なものにはテキストを書き、ただの装飾であれば`""`(空)にする
  * 根拠：記述なしは構文エラー。チェッカーを通せば出るが、よく見るので特筆した
* img要素は仕様としてdiv、figure、picture要素などを親として囲ってもいいし、囲わなくてもどちらでもいい。無意味にネストを深くしないという目的では後者
* 画像のレスポンシブ対応はimg要素・srcset属性/sizes属性やpicture/source要素を用いる
* section要素はbody要素などセクショニングルートの直下の子要素として使用不可
  * 根拠：セクショニングルートはアウトラインを形成するため、section要素(セクショニングコンテンツ)と機能重複する
  * 参考：<https://developer.mozilla.org/ja/docs/orphaned/Web/Guide/HTML/Using_HTML_sections_and_outlines#The_HTML5_outline_algorithm>
* section要素は子・子孫要素にh(x)要素を含まなければ使用不可
  * 根拠：見出しなしセクションは推奨されていない
  * 参考：<https://html.spec.whatwg.org/multipage/sections.html#the-section-element>
* article要素は「独立した意味のある記事」に用いる。要約・切り出しコンテンツやブログ記事へのリンクラップ要素などで使っている例を見るがそれらは定義上誤り
* ul、ol要素の直下にはli要素しか置けない。ほかはすべて構文エラー
* dl要素の直下にはdivが置ける

* アクセシブルなマークアップを心がける
  * HTMLの要素(タグ)では表現しきれないアプリケーションUIやウィジェット機能は、「WAI-ARIA」のrole属性とaria-*属性で補完する
  * 例. 検索バーは`role="search"`、タブUIは`role="tablist"`、`"tab"`などなど
  * 詳しい種類はこちらを参照：<https://developer.mozilla.org/ja/docs/Web/Accessibility/ARIA/ARIA_Techniques>

#### Web(HTML)テンプレートエンジンの使用有無

* Web(HTML)テンプレートエンジンは積極的・能動的に使用しない。素のHTMLが結局扱いやすく、見通しやすいため
* Webアプリケーションフレームワークやライブラリ上で機構として組み込まれたものや、ファイル構成上の利点が多い場合はこの限りではない
  * Node.js(/Express)アプリケーションにおける[EJS](https://ejs.co/)
  * Ruby on RailsにおけるERB、PHP系フレームワークにおける[Twig](https://twig.symfony.com/)
  * ほかには[Handlebars](https://handlebarsjs.com/)、[Nunjucks](https://mozilla.github.io/nunjucks/)
  * Pug、Blade、Slim、Smarty、Edge.jsは個人的には選択しません

### CSS

#### 標準仕様書

* 「Cascading Style Sheets」by W3C
  * <https://www.w3.org/Style/CSS/>

#### 推奨チェックツール

* stylelint(エディタ拡張機能およびnpm module)
* W3C Validator(エディタ拡張機能)
* 「W3C CSS 検証サービス」で構文チェックおよび可能な範囲でのエラー修正をする。古いツールなので念のためくらい
  * <https://jigsaw.w3.org/css-validator/#validate_by_uri>


#### 推奨フォーマッター

* Prettier(エディタ拡張機能およびnpm module)利用OK
  
#### 規約

* CSSスタイルはclassセレクタ指定を原則用いる
  * classセレクタの子や子孫として、必然性のある要素セレクタ(`.class(ul) > li`)や属性セレクタ(`[aria-*]`、`[data-*]`含む)指定は問題ない
  * idセレクタでのスタイルはその役割面や詳細度問題から原則推奨しない
* リセットCSSは古過ぎない仕様のものであれば使用OK
* `!important` の利用は避ける。動的にスタイルを付け替える際は仕方ない場合もあるが極力回避する
* 変数には[CSS Custom properties](https://www.w3.org/TR/css-variables-1/#defining-variables)を利用
  * 根拠：標準CSSで使えることから、Sassなどプリプロセッサでの変数定義はほぼ無意味なので使用しない
* CSS単位の指定には`rem`/`em`または`%`を積極的に使う。viewport基準単位(`vw`/`vh`/`vmin`等)もOK。絶対単位`px`は使っても良いが推奨しない
  * 根拠：<https://crestadesign.org/unit/#pxemremvw-2>
* CSSショートハンド記法は使ってもいいが、1プロパティの指定で用いない、また重ねがけしない
  * NG例： `margin: 2rem auto auto;`
  * OK例： `margin-block-start: 2rem;`
* CSSプリプロセッサ言語は最もメジャーと思われるSass・SCSS記法(拡張子.scss)を用いる
* 新規プロジェクトの場合、SassコンパイラはDart Sassを利用する(2021/12現在)
  * 根拠：公式にてメジャー版として推奨されている
    * <https://sass-lang.com/blog/libsass-is-deprecated>
* Sass利用時のコメント記法の書き分け
  * 「`/* */`」はCSSコンパイルファイル上に残す前提で使用
  * 「`//`」はSass独自設定のみに使用する。コンパイルファイルに残らない

#### CSS設計

* CSSのグローバル汚染が起きなければ基本どんな構成、ルールでもOK
* 基本的には、設定ファイル群(baseディレクトリ)とそれ以外のUIモジュール/コンポーネントファイル群(generalディレクトリ)の2構成がシンプルかつ必要十分だと思っている
  * 命名規則は[BEM](http://getbem.com/)に近いものであれば最大公約数的に良いと思われる
  * 名前空間・接頭辞(`.home-*`、`.about-*`、`.header-*`、`.hero-*`など)で縛るのはアリ
  * ECSS、rscssの記法を取り入れてもOK
* そのほか、CSS Modules、Scoped CSS、CSS in JSなどのCSS技法・機能も、プロジェクト特性に応じ1プロジェクトにつきいずれか1つを導入可とする

#### CSSフレームワークやフロントエンドライブラリ(ReactコンポーネントやVueフレームワーク含む)の利用について

* 要件を満たせれば利用に関しては問題ないが、パフォーマンス(ファイル容量)やコード可読性をいたずらに低下させないことを旨とする

### JavaScript

#### マストチェック

* 「Webブラウザの開発者ツール(ChromeならDevTools)」でConsoleエラーが発生していないかを必ず確認する
* その上でJavaScript由来の機能が動作しているかを仕様と目視で照らし合わせて問題なければOK

#### 推奨チェックツール

* ESLint(エディタ拡張機能およびnpm module)
* JShint(Webサービスおよびエディタ拡張機能)
  * <https://jshint.com/> ※ちょっと古い

#### 推奨フォーマッター

* Prettier(エディタ拡張機能およびnpm module)利用OK

#### 標準仕様書

* 「TC39 - Specifying JavaScript.」by Ecma International
  * <https://tc39.es/>
  * 日本語訳：<https://tc39.es/ja/>
* 補足的な解説書：「MDN Web Docs」by Mozilla
  * <https://developer.mozilla.org/ja/docs/Web/JavaScript/Language_Resources>

#### 規約

* 以下2つのJavaScriptコーディングガイドラインを基準として扱う。矛盾する部分を除いて基本的事項を以下に列挙する
  * 「JavaScript guidelines - MDN」by Mozilla
    * <https://developer.mozilla.org/en-US/docs/MDN/Guidelines/Code_guidelines/JavaScript>
    * 基本・空白
      * 1行あたりの行数は80文字以下に収める
      * 関数やオブジェクトなどの定義ブロックの前後は空行で区切る
      * 2項演算子は空白で区切る
      * カンマ/セミコロン、キーワードの後方には空白を含める(ただし行末の空白は不要)
    * 命名
      * 変数/関数名は先頭小文字のcamelCase形式
      * 定数名はすべて大文字のアンダースコア形式
      * コンストラクター/クラス名は先頭大文字のCamelCase形式
      * プライベートメンバーは「_」で始める
    * その他
      * すべての変数は宣言、初期化すること
      * 変数の宣言が重複しないこと
      * 配列、オブジェクトの生成には、`[...]`、`{...}`などのリテラル構文を利用すること
      * 真偽値をtrue/falseと比較しない
      * 条件判定には、等価演算子(`==`)ではなく、厳密等価演算子(`===`)を用いる
  * Google JavaScript Style Guide
    * <https://google.github.io/styleguide/jsguide.html>
    * 主な規約
      * セミコロンは省略しない
      * 文字列のくくりには「"」よりも「'」を優先して利用する
      * 基本データ型(stringやnumber、booleanなど)のラッパーオブジェクトは使用しない
      * 名前空間を利用して、グローバルレベルの名前は最小限に抑える
      * ビルトインオブジェクトのプロトタイプは書き換えない
      * with/eval命令は利用しない
      * for...in命令は連想配列/ハッシュでのみ利用する
* TypeScript(JavaScriptスーパーセット)は利用してもOKだが要検討
  * 高確率で"ネイティブJavaScriptでの実装工数のほうがTypeScriptでの実装工数より少ない"ケースが多い
  * 長期的に型安全などメリットが大きいと判断できれば利用OK
* jQuery利用は基本推奨しないが、場合による
* ネイティブJavaScript配布ライブラリは、動作が担保・検証できれば利用OK
  * 選定基準：極端にマイナーなものでない
* React、Vue.jsベースのフレームワーク(Next.js、Nuxt.jsなど)の利用はプロジェクト特性から問題なければ積極的に利用する場合がある

### メディア (画像・音声・動画など)

### フォント

#### システムフォント

* メリット：Webページの表示パフォーマンス観点から、フォントはすべてシステムフォント指定とすることの意義・効果は大きい
* デメリット：硬めの雰囲気を持つフォントが多いため、文字によるデザイン表現性に幅が出しにくい
* 個人的な基本フォント指定はすべてシステムフォントが前提(2021)
  * `Helvetica Neue, Segoe UI, Arial, Hiragino Kaku Gothic ProN, Hiragino Sans, BIZ UDPGothic, Meiryo, sans-serif;`
  * 参考記事：<https://ics.media/entry/200317/>
  
#### Webフォント

* メリット：文字によるデザイン表現性の幅が広がる。Webページの雰囲気が豊かになる。Noto Sansなどとても可読性が高いフォントもある
* デメリット：日本語(和文)Webフォントは軽量化を図ってさえファイルサイズが重いため、致命的なパフォーマンスボトルネックになり得る。基本的に使用を避けたい
* 欧文Webフォントの利用は1~2ウェイト程度ならパフォーマンス的にはさほど問題なさそう
* 推奨するWebフォントの読み込み方 - CSS @font-face
  * <https://github.com/ishimasar/pattern-library/blob/main/src/assets/scss/base/_font-face.scss>

### Webアクセシビリティ

#### 推奨チェックツール

* AXE Accessibility Check(エディタ拡張機能およびnpm module)
* WAVE Web Accessibility Evaluation Tool(Chrome拡張機能)
* A11yc アクセシビリティ チェック サービス(Webサービス)
  * <https://a11yc.com/check/index.php>

#### 標準仕様書

* 「Web Content Accessibility Guidelines (WCAG) 2.1」by W3C
  * <https://www.w3.org/TR/WCAG21/>

### パフォーマンス

#### 推奨チェックツール

* PageSpeed Insights(Webサービス)
  * <https://pagespeed.web.dev/>
* Lighthouse(Chrome拡張機能)
* GTmetrix(Webサービス)
  * <https://gtmetrix.com/>

#### 最適化

* HTMLのscript要素はdefer(解析系はasync)属性を付与した上で、head要素内に記載する
  * これによりレンダリング阻害が緩和される
  * 用途によってhead要素内に記述できないスクリプトもあるので上記の限りではない
* 描画パフォーマンス寄与のため、link要素のpreroad属性、Resource Hints API(prefetch、preconnect属性など)をアセットへ適切に適用する
* コードファイルおよび画像、動画、音声、Webフォントといったバイナリファイルは最適化処理をしてから納品する
  * フォーマットごとに何かしらの最適化ツールがあるので使う
  * WebPフォーマット画像の利用とともに、PNG/JPEGフォールバック(picture、source要素)も用意する(2021現在、Safariがまだ完全対応でないため)
  * 画像、動画、音声、Webフォントファイルはプロジェクト内で極端にディレクトリに小分けせず、シンプルに
  * 一定以上サイズの画像と日本語(和文)Webフォント利用は、致命的なパフォーマンスボトルネックになり得るので要注意

### ビルドツールとバージョン管理

#### フロントエンドビルドツールの利用について

* webpack、parcel、viteなどのビルドパッケージ、またはNext.js、Nuxt.js、Svelte、GatsbyなどのJSフレームワーク類、いずれも利用は特に問題ない。そのプロジェクトにふさわしいと思われるものを選定することを旨とする

#### バージョン管理ツール

* Git + GitHubを利用
* 開発ワークフロー：基本GitHub Flowで行う。場合に応じてgit-flowやカスタマイズを適用する

### デバイスおよびOS別ブラウザチェック - 品質検証

#### 納品直前に必ず品質検証(QA)を実施する

#### 必須検証条件

* 要件および仕様を満たしていること
* デザイン指定に対して画面上での表示崩れがないこと
* 閲覧不可でないこと
* 意図しない不正常な挙動がないこと
* 致命的なコードエラーがないこと
* 著しい閲覧しにくさ、使いにくさがないこと

#### 基本対象範囲(2021/12時点)

* Windows10(11)
  * Google Chrome最新版、Micrsoft Edge最新版
* macOS X
  * Google Chrome最新版、Safari最新版
* iPhone10~15(iPhoneOS、iOS)、iPad最新あたり
  * Google Chrome最新版、Safari(on iOS)最新版
* Android v8~12(AndroidOS)
  * Google Chrome最新版

### その他

#### 提供言語 (ローカリゼーション)

#### Deployment / Integration

#### コードレビュー方針

* GitHub Pull Request機能を用いて、主にレビューを行う
  * レビューイ(レビューを受ける側)はコーディングの目的を明確化して作業し、レビュアー(レビューをする側)に伝達する
  * レビュアーは当該作業の目的を的確に把握して、目的達成の観点からレビューする
    * 枝葉や関係のない部分の指摘は無闇に行わない。目的と関係ない部分で必要性がある場合は別途タスクとして切り出す
    * 緊急性に応じて、main branchからfix/hotfix branchを作成して対応
  * レビュアーはレビュー依頼に極力迅速に反応する(すぐレビューできない場合もそのことを伝える)

---

### 命名規則

### 命名の考え方

### ファイル命名

#### 対象：コード/テキストファイル、ディレクトリファイル(フォルダ)、メディアファイル(画像、動画、音声、フォント)

* 基本的に英文小文字(lower case/ローワーケース)
  * 通しorバージョン番号として数字使用OK(`xx-01`、`xx-02`...)
* ハイフン(-)つなぎで統一。アンダースコア(_)つなぎ禁止
* 利用しているフレームワーク/ツールの仕様によってはこの限りではない

### CSSセレクタ命名 (class、id)ほか

#### ECSS + rscssを採用

* ECSS公式：<https://ecss.benfrain.com/>
* rscss公式：<https://rscss.io/>

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