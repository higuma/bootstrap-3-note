Bootstrap 3 学習ノート
========================================================================
(2014-06-09 ... 18)

> Bootstrap 3の学習記録ノートです。
> 
> できるだけ手を抜かず隅々まできちんと調査し、コードはほぼ全て実際に試して確認しました。
> 
> 元々公開を意図したものではありませんが、ここまで詳細に調べた資料はそうはないと思いますので最低限の体裁を整えて公開します。みなさんのお役に立てば幸いです。
> 
> なおHTML部分はほぼ全てjadeで記述しています。jadeを知らないと理解できないノートになってしまっていますが、生のHTMLではとてもこのスピードでは学習できません。どうかご了承下さい。
> 
> なお「ここは違うのでは」「こうした方がよいのでは」などという点がありましたらGitHubのissuesかpull requestなどでお教え頂けるとありがたいです(6/19記)。


はじめに
========================================================================

Bootstrapは以前(2の頃)少しだけ経験があるが、この辺で本格的に学んで完全に使いこなせるようになっておく。

<http://getbootstrap.com/>

Bootstrap 3は2と互換性はない(よく知られている)。今でも検索するとBootstrap 2の解説サイトが大多数で3は少ない。しかしv3リリース(2013-08)からもうすぐ1年になる。今本気で勉強するなら迷わず3だろう。

オフィシャルサイトの内容も現在は全て最新版(3.1.1)に統一されている。昔のサイトもまだ残してあるが(下記url参照)、今回は最新版に集中する(基本的に後方互換は考慮しない)。

<http://getbootstrap.com/2.3.2/>

> (参考) Bootstrap 3の日本語解説を見つけた。Bootstrap 2の解説はたくさんあるが、3はまだ少ないのでここに残しておく。
> 
> * <http://c.hrgrweb.com/bootstrap3/index.html>
> * <http://bootstrap3.url.ph/>


Getting Started
========================================================================
<http://getbootstrap.com/getting-started/>

## Download

CDNを利用できる。

``` html
<link rel="stylesheet" href="//netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap-min.css">

<!-- Optional theme -->
<link rel="stylesheet" href="//netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap-theme.min.css">

<!-- Latest compiled and minified JavaScript -->
<script src="//netdna.bootstrapcdn.com/bootstrap/3.1.1/js/bootstrap.min.js"></script>
```

今回は特別なツールは使わずGitHubのzipballをdownloadする。

<https://github.com/twbs/bootstrap>

> Bower(って何?)でインストールしなさいと書いてあるがこれはtwitter製パッケージマネージャ(npmの後継?)。検索するといろいろ便利らしいが今回は略(覚えることが多過ぎてもう...)。

## What's included

現バージョンは3.1.1だが、今回のように純粋に単に利用するだけの場合はdist/の中だけ利用すればいい。ここに実行時用ファイル一式がある。またdocs/の中にドキュメント一式がある。

> GitHub repoから昔のバージョン(全てのcommit)をダウンロードできる。以下はその一例(git cloneして自分でコマンド操作するより簡単)。
> 
> * `branch: `ドロップダウンからtags v2.3.2を選択
> * ページがその時点の内容に切り替わるので、`Download ZIP`でダウンロード

## Basic template

ひな形は次の通り(ほぼそのままコピペ)。

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap 101 Template</title>

    <link href="css/bootstrap.min.css" rel="stylesheet">
    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and
         media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>Hello, world!</h1>
    <p>ここが本文(contents)</p>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```

> ソースコメントにある通りrespond.jsはローカルコピーしたものを使うと機能しない(ただし今IEを使ってないので未確認)。リクエストに対してサーバがブラウザ判定して個別対応する部分があるらしい。

前半部分のHTML5 shimとRespond.jsの部分は少し注意。最近はJavaScript読み込みをbodyの最後に置くのが流行だがこれらは例外で、bodyより前にないと機能しない。

``` html
<!--[if lt IE 9]>
<script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
<script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->
```

HTML5 shim(shiv)は古いブラウザでHTML5用要素を認識させる(これは知っているので略)。またRespond.jsはCSS3のmedia queryに対応するもの。

<https://github.com/scottjehl/Respond>

Respond.jsは次の解説を参照。ただし今回は深くは立ち入らない。使うだけならテンプレートのコピペで十分だし、もし必要が生じたらその時詳しく調べればよい。

<http://lab.informarc.co.jp/javascript/ie_responsive_webdesign.html>

以下時間短縮とケアレスミス防止(特にネストレベルの認識)のためHTMLソースは全てjadeで記述する。しかしIEの条件コメントをjadeでどう書けばいいかが分からない。jadeのリファレンスは次の通り。

<http://jade-lang.com/reference/>

リファレンスを見てもこんな特殊ケースはさすがに記述がない。調べてみたら次を見つけた(ありがとう!)。

<http://qiita.com/sasaplus1/items/189560f80cf337d40fdf>

実はそのまま書けばよい(何だそういう事か)。次のコードでjadeは意図通り出力した。

``` jade
<!--[if lt IE 9]>
script(src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js")
script(src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js")
<![endif]-->
```

それから後半部分にも注意。BootstrapはJavaScriptコードがないと完全には動かない(dropdownメニュー等)。またjQueryを利用しているので先に読み込んでおく必要がある。これら2つはbodyの最終部分に置く。jadeのコードは次の通り。

``` jade
script(src="//ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js")
script(src="//netdna.bootstrapcdn.com/bootstrap/3.1.1/js/bootstrap.min.js")
// (その後application.js等)
```

## Examples

いろいろな例(確認したのはほんの一部だけ)。後で自分でいろいろ作る時に適宜参考にする。

## Community

...ここに書いてあるのより、やっぱりGoogle先生だよなあ...(以下略)。

## Disabling responsiveness

> ここから先はもう"getting started"ではなく高度な内容(最初はスキップしてCSSに進んだ - 全部読み終えて最後にここを読み返しているところ)。

ここでのresponsivenessとは画面サイズに応じてレイアウトを変化させる機能を指している。場合によってはこれを使いたくない状況もありうるのでその方法を示している。詳しくは"Steps to disable page responsiveness"のinstructionを参照(略)。

> CSSページの先頭に関連する設定があるが、特にモバイル端末用設定に微妙なissuesがある。ここはまだ深入りしない。

Bootstrap 2のプロジェクトを3に変換する場合は次を参照(特に前半部分が2から3へのclass対応表)。

<http://getbootstrap.com/migration/>

## Browser and device support

対応状況は表の通り。IEは8以上で対応している。

その先はIEを中心とする環境別の細かい注意点。これは将来何かが完成してそれを(特にIEで)テストした時に問題が生じたら読むような部分なので今はまだスキップする。

## Third party support

ここは他の環境(API)とのconflictに関するissuesで、具体的にはGoogle MapsやGoogle Custom Search EnginesとCSS設定(box-sizing)がぶつかる問題の解決方法(略)。

## Accessibility

障害者支援機能の説明。

> Assistive technology(AT)に対応する日本語はまだなく(考えてる人はいるはずだが普及している用語はない)、あえて訳せば「障害者支援技術」。日本語だと今はまだ「障害者」という言葉を省略すると何の意味か分からないだろう。
> 
> > 最近は「障がい者」という表現が多い。配慮はもちろん理解できるが、何か表現の自由を剥奪しようとする(悪しき?)意思のようなものが...

今は全部読み終えてここを読み返しているところ。もう全て意味は分かる。

* .sr-only(スクリーンリーダ使用時のみ表示)はexampleにたくさん出てくる
    * ちなみにaria-\*という属性もexampleによく出てくる(WAI-ARIA由来)
* h1(原則先頭に一つだけ)から階層構造にするのは基本(自分は大体従っている)
    * AT対応という面ではできるだけ細かく付けるべき
* ただし開発途中にいちいち対応するのはちょっと効率が悪いと思う
     * (参考) AT対応ツールみたいなのがあるといい
        * 対応が必要な部分を検出して
        * 必要なHTML markupを補間する

> (参考) WAI-ARIA仕様書
> 
> * 原文: <http://www.w3.org/TR/wai-aria/>
> * (古い)和訳: <http://www.hitachi.co.jp/universaldesign/ria/ajax/wai-aria/index.html>
> 
> またAT対応ツールというのは有力なアイデアだが今の自分の立場では作る気にならない(ツールを作成するより仕様書を読んでひとつひとつ手書きした方が現実的)。ここはTwitterが純正ツールを作るべきと提案する。
> 
> > Twitter様: もしそのようなお仕事を頂けるなら考えます...

## License FAQs

ライセンスはMIT。要求事項は著作権表示のみで、それ以外に制限事項はない。以下書いてあることは全て常識の範囲なので略。

## Customizing Bootstrap

MITライセンスでGitHubに全情報を公開しており、ソースを直接書き換えて自由に使っていい。ここはもう少し簡単に自分で少しCSSを加えて元の設定をoverrideする方法を説明している。

本文はカスタムボタンだが、ここはもっと簡単にnavbarの色だけ変えてみる。まずCSS側はbootstrap.cssの後に次を加える。

``` jade
  style(type='text/css').
    .navbar-skyblue { background-color: skyblue; }
```

HTML側はnavbarにこのクラスを追加すればよい。この程度なら誰でもできるだろう。

``` jade
  nav.navbar.navbar-default.navbar-skyblue
    div.container-fluid
      a.navbar-brand(href="#") Title
```

## Translations

日本語訳は(まだ)ない。

> 和訳作成プロジェクトがあるかも知れないが完成まで待つ訳にはいかない。それにこういう文書は足が早いのでどうせ2年もすれば古くなる。結局(たとえ和訳があっても)原文を読むのが一番の近道。

------------------------------------------------------------------------

(以下参考)

ドキュメントを全文検索するにはdoc/ディレクトリの中をgrepで探せばいい。しかしBootstrap 3からドキュメントにJekyllが導入されており、docs/の中のドキュメントをそのままブラウザで立ち上げることができない(2の頃はそのままブラウザで読み込めた)。

JekyllはWebページ生成ツールで、特にBlogなどのサイト構築に用いられる。

<http://jekyllrb.com/>

これはgemなのでちょっと試してみる。

```
$ gem install jekyll
```

BootstrapのGitHub repoのディレクトリに移動して次を実行するとローカルサーバを立ち上げる(localhost:9001)。

```
$ jekyll serve
```

> 次はJekyllの解説(もし将来Jekyllを使う機会があれば読む)。
> 
> <http://melborne.github.io/2012/05/13/first-step-of-jekyll/>
> 
> 流れとしてはまずstatic埋め込みエンジンのLiquidがあり、それを利用したサイト構築ツールがJekyll、Jekyllをベースとしてそれをさらにブログに特化したのがOctopress。

ちょっと脱線した。元はと言えば文章を全文検索したかっただけなのだが、jekyllを使っているため実際のサイトとは異なる場所のファイルにヒットする。そこでjekyllを調べ始めたところ変な方向に行ったので本来の目的に戻る。

例えばdocs/components.htmlの内部は次のようになっており、別のファイルを読み込んでいる。

```
...
{% include components/navs.html %}
{% include components/navbar.html %}
{% include components/breadcrumbs.html %}
...
```

これらの文章はdocs/\_includes/の中にあり、docs/\_includes/components/navbar.htmlなどのファイルを読み込んでいる。よって全文検索したければdocs/_includes/の中をgrepすればよい。

```
$ grep -rl list-group-item docs/_includes       # 例
```

最初は何かclass一覧のようなものがありそれを覚えればいいくらいに考えていたが、実はそんなに甘いものではない(後で思い知った...)。結局公式ドキュメントを順に読むことにした。

> 検索したら次を見つけた。でもこれは単にクラス名を抜き出しただけなのであまり訳に立つものではない(これくらい自分でも生成できそうだし...)。
> 
> <https://gist.github.com/geksilla/6543145>
> 
> もうひとつ見つけた。こちらの方がよさそう。
> 
> <https://gist.github.com/Integralist/1391440>
> 
> しかしBootstrapは要素の入れ子のパターンとclass設定の組で機能するものなので、単純な一覧表にするのは難しい(仮に作っても役に立つかどうか...)。

------------------------------------------------------------------------


CSS
========================================================================
<http://getbootstrap.com/css/>

## Overview

* doctypeはHTML5形式の`<!DOCTYPE html>`(jadeでは`doctype`)
* `<html lang='en'>`と記述しなさいと書いてある
    * lang="en"を要求する意味はだいたい分かる
        * 縦書きやアラビア文字(右から左)には対応困難(そういう作りではない)
        * その他万が一にもレイアウト設定に影響しないように限定したい
    * しかしこれでは英語ページ以外では何か副作用がありそう
        * semanticsの面から考えるとこれは本来「やってはいけない」事だろう
        * これをW3Cの人が見たら怒るのでは...
    * 横書きの日本語サイトであれば従う必要なしと自主判断する
        * 実際これに従っている日本人はほとんどいない模様
* 次はモバイル向けの設定
    * `<meta name="viewport" content="width=device-width, initial-scale=1">`
    * しかしどうもいろいろ問題ありそう - 次の考察を参照(でも深入りしない)
        * <http://blog.ousaan.com/index.cgi/links/20130925.html>
* コンテンツは全体を(div).containerで囲う
    * div.containerはネストしないこと(そういう風に作られていない)

## Grid System

最初はまとめ。

* grid systemは12列に縦分割する画面モデル
* (div).containerは固定幅レイアウトコンテンツの外側の囲み
    * CSS media queryを用いて画面幅を取得
    * 幅を4通りに分類し、それより一回り小さい固定幅にする
    * 4通りのclass prefixがある
* (div).container-fluidに変更すると横画面いっぱいに取る
* .container(-fluid)の内部に.rowを作り
    * 内部に.(prefix)-(1..12) のクラスを設定すると配置する
* (.containerと異なり).rowはいくらでもネストしていい

ここでCSSリファレンスを調べてみる。やはり次が一番実用的かな(見慣れているし...)。

<https://developer.mozilla.org/en-US/docs/Web/CSS/Reference>

@mediaの説明は次を参照。ここにはmedia queryの詳しい解説がないが、W3Cリファレンスへのリンクがある。

<https://developer.mozilla.org/en-US/docs/Web/CSS/@media>

> 経験則だがこういう場合はMozillaのドキュメントから探した方がGoogleで直接W3CやWHATWGドキュメントを検索するよりだいたい早く見つけられる。

次のW3Cリファレンスを参照(example 5付近の内容が近い)。今のところlessのソースをいじくる気はないが、知っていればbootstrap.cssを読む時に困らない。やはり最低限知ってた方がいい(ただし深入りは禁物)。

<http://www.w3.org/TR/css3-mediaqueries/#media0>

BootstrapはCSS media queryを使って画面の横幅(px)を取得し4通りに判別する。.containerの幅は実際の幅より一回り小さい固定幅に設定される。

* 1200px以上: containerは1170px、クラスは`.col-lg-` (PCフルスクリーン?)
* 992..1199px: containerは970px、クラスは`.col-md-` (PC向け)
* 768..991px: containerは750px、クラスは`.col-sm-` (タブレット向け)
* 768px未満: containerは実サイズに対して可変、クラスは`.col-xs-` (スマホ用)

> それぞれLarge(lg), Medium(md), Small(sm), Extra small(xs)の略。

次の例は横幅992以上でgrid systemが有効になり横を12等分して表示する。それより小さいと普通のdivと同じように上から下に表示する。

``` jade
div.container
  div.row
    - for (var i = 0; i < 12; ++i)
      div.col-md-1 .col-md-1
  div.row
    div.col-md-8 .col-md-8
    div.col-md-4 .col-md-4
```

> .col-md-を設定するとその時点で992px以上では列の幅が固定値(mdの場合は78px)に設定される(992未満の場合は上から下に表示)。そのためlgが成立する場合でもmdの幅のページとして扱われる。

複数の表示環境(典型的にはPCとスマホ)に対応させる場合は複数のクラス設定を行う方法がある。次の例では992px未満では.col.xs-6が適用され一行に2列、992px以上では,col-md-4が適用され3列になる。

``` jade
div.container
  div.row
    - for (var i = 0; i < 6; ++i)
        div(class="col-xs-6 col-md-4") .col-xs-6 .col-md-4
```

次のclearfixというのはCSS上級者なら誰でも知っているテクニックのようだ。自分も名前くらいは知っていたが今回はちょっと調べてみる。

------------------------------------------------------------------------

(以下は参考: clearfixミニ講座)

まずは次を参照。

<http://blog.d-spica.com/entry/070307clearfix.html>

段組をfloatで行う場合、親divのbox高さはfloatしていない要素の高さで決められるため時々困ったことになる。以下は典型的な2段組ページの例。div.wrapperは全体を覆って欲しいのにfloatでない要素の最大高さまでしか覆ってくれない。

```
+------------ div.wrapper -----------+
|+-------------------++-------------+|
||                   ||             ||
||   div.content     ||  div.menu   ||
||   (float:left)    || (non-float) ||
||                   |+-------------+|
+|-------------------|---------------+
 |                   |
 +-------------------+
```

もちろんdiv.wrapperは全体を覆って欲しい(特に背景に色や画像などを設定している場合)。この場合の常套テクニックとして一番下に何か要素を置き、CSSで`clear:both`を指定し回り込みを解除する。

```
+------------ div.wrapper -----------+
|+-------------------++-------------+|
||                   ||             ||
||   div.content     ||  div.menu   ||
||   (float:left)    || (non-float) ||
||                   |+-------------+|
||                   |               |
||                   |               |
|+-------------------+               |
|+----------------------------------+|
||      div.clear (clear:both)      ||
|+----------------------------------+|
+------------------------------------+
```

これでdiv.wrapperは全体を覆ってくれた。もしステータスバーみたいなのが本当に必要なら幸運だが、そうでなければ空の(またはそれに近い)ダミーコンテンツを記述しなければならない。

> 今でも一番下にCopyrightや(メインではない)サブメニューを置いているサイトはとても多い。潜在的な理由としてこの事情があるみたいだ。

これがclearfixが必要な状況で、ダミーのHTML要素を下に置くのはsemantics的に望ましくない(とまでは自分は思わないが、こう書いてある解説は時々見つける)。そこでHTML側ではなくCSSの:after擬似要素を利用して解決する。

``` css
.clearfix:after {
  content: ".";     /* 新しい要素を作る(""だと認識しないブラウザがある) */
  display: block;   /* ブロックレベル要素に */
  clear: both;      /* ここが核心部 */
  height: 0;            /* ここと次で表示を抑制するが...昔は... */
  visibility: hidden;   /* ブラウザ仕様(バグ?)の対応が大変だった... */
}
```

今では理解困難な設定もあるがその多くは古いブラウザ仕様やバグの対応らしい。これをwrapper要素のclassに追加する。結果は次の通り。

```
+------- div.wrapper.clearfix -------+
|+-------------------++-------------+|
||                   ||             ||
||   div.content     ||  div.menu   ||
||   (float:left)    || (non-float) ||
||                   |+-------------+|
||                   |               |
||                   |               |
|+-------------------+               |
+------------------------------------+ <== :afterはここに適用
```

更に詳しい解説がこちら(上記解説もここから見つけた)。昔のブラウザのバグまで考慮したコードだということも理由付きで書いてある(実に奥深い...)。しかし今ではここまで理解する必要もないと判断し参考とする。

<http://kojika17.com/2013/06/clearfix-2013.html>

今はもうこれを自分で書くのではなく、信頼できるライブラリに任せたい。今回はBootstrapにやってもらう。

------------------------------------------------------------------------

Bootstrapの.clearfixの解説は次の通り。これは大昔のブラウザを多少切り捨てたmicro clearfixという方法を使っている(上記詳細解説にも説明あり)。

<http://getbootstrap.com/css/#helper-classes-clearfix>

もうひとつResponsive utilitiesも(後で出てくるが)ここで予習する。

<http://getbootstrap.com/css/#responsive-utilities>

それでは本文のexampleを確認するが、実は本文そのままではclearfixはあってもなくても同じ結果になってしまうので位置を変更した。.clearfixは「ここでfloat解除」、.visible-xsは「XS幅の場合のみvisible(有効)」。

> clearfixは上で示した例の書き方と少し異なり、wrapper(content)ではなくここからfloatを解除する要素に対して用いる。

``` jade
div.container
  div.row
    div.col-xs-6.col-sm-3 .xs-6.sm-3
    div.col-xs-6.col-sm-3 .xs-6.sm-3
    div.col-xs-6.col-sm-3 .xs-6.sm-3
    div.clearfix.visible-xs
    div.col-xs-6.col-sm-3 .xs-6.sm-3
```

横幅が768以上(sm)だと横に配置する(clearfixは効かない)。

```
.xs-6.sm-3    .xs-6.sm-3    .xs-6.sm-3    .xs-6.sm-3
```

横幅を768未満に変更すると.clearfixが有効化されて次のように配置する。

```
.xs-6.sm-3    .xs-6.sm-3        <= xs-6なのでまずここで改行
.xs-6.sm-3                      <= ここでclearfix
.xs-6.sm-3
```

次はgrid optionだが、exampleにはまともな説明はない(学習者泣かせ)。まずは最初の例から何をやっているか探る。

``` jade
div.container
  div.row
    div.col-sm-5.col-md-6 .col-sm-5.col-md-6
    div.col-sm-5.col-sm-offset-2.col-md-6.col-md-offset-0
      | .col-sm-5.col-sm-offset-2.col-md-6.col-md-offset-0
```

ここでのpointはcol-XX-offsetの使い方。PC幅(md)だと次のように表示する。md-offset-0なので間は空かない。

```
+----------------------------------+----------------------------------+
|.col-sm-5.col-md-6                |.col-sm-5.col-sm-offset-2.col-md- |
|                                  |6.col-md-offset-0                 |
+----------------------------------+----------------------------------+
                                   ^
                                   |
                          ここが中央(6:6で等分)
```

タブレット幅(sm)では次の通り。sm-offset-2が有効になり間に2グリッドの空間が挿入される。

```
           (5)                (2)             (5)
+--------------------------+       +--------------------------+
|.col-sm-5.col-md-6        |       |.col-sm-5.col-sm-offset-  |
+--------------------------+       |2.col-md-6.col-md-offset- |
                                   |0                         |
                                   +--------------------------+
```

次の例(今度は3通り)。md-offset-2は「md以上でoffset 2」という意味なのでlgでそれをキャンセルするためのlg-offset-0が必要。

``` jade
div.container
  div.row
    div.col-sm-6.col-md-5.col-lg-6 .col-sm-6.col-md-5.col-lg-6
    //                                            ここに注意(必要)
    //                                            vvvvvvvvvvvvvvvv
    div.col-sm-6.col-md-5.col-md-offset-2.col-lg-6.col-lg-offset-0
      | .col-sm-6.col-md-5.col-md-offset-2.col-lg-6.col-lg-offset-0
```

```
smの場合
+--------------+------------+
|      (6)     |    (6)     |
+--------------+------------+

mdの場合
+-------------+     +-------------+
|     (5)     | (2) |     (5)     |
+-------------+     +-------------+

lgの場合
+----------------------+----------------------+
|           (6)        |          (6)         |
+----------------------+----------------------+
```

次の例はoffsetの説明用(もう分かったようなもの)。

``` jade
div.container
  div.row
    div.col-md-4 .md-4
    div.col-md-4.col-md-offset-4 .md-4.md-offset-4
  div.row
    div.col-md-3.col-md-offset-3 .md-3.md-offset-3
    div.col-md-3.col-md-offset-3 .md-3.md-offset-3
  div.row
    div.col-md-6.col-md-offset-3 .md-6.md-offset-3
```

```
+---+---+---+---+               +---+---+---+---+
|       4       |       4       |       4       |
+---+---+---+---+               +---+---+---+---+
            +---+---+---+           +---+---+---+
      3     |     3     |     3     |     3     |
            +---+---+---+           +---+---+---+
            +---+---+---+---+---+---+
      3     |           6           |     3
            +---+---+---+---+---+---+
```

ネストする場合は内側をさらに12分割する。

``` jade
div.container
  div.row
    div.col-md-9 Level 1: .col-md-9
      div.row
        div.col-md-6 Level 2: .col-md-6
        div.col-md-6 Level 2: .col-md-6
    div.col-md-3 Level 1: .col-md-3
```

```
+---------------------------------------------+-----------------+
|Level 1: .col-md-9                           |Level1: .col-md-3|
|+---------------------+---------------------+|                 |
||Level 2: .col-md-6   |Level 2: .col-md-6   ||                 |
|+---------------------+---------------------+|                 |
|                                             |                 |
+---------------------------------------------+-----------------+
```

push/pullを使って順番を入れ替えられる。しかし本文にはほとんど説明がないので解析を試みる。わざとちょっと複雑にしてみた。

``` jade
div.container
  div.row
    div.col-md-3.col-md-push-7 .3.push-7
    div.col-md-3.col-md-pull-1 .3.pull-1
```

出力は次の通り(実際にはこういう配置に出力しようとしてpullとpushの値を調整して上記ソースになったもの)。

```
        +---+---+---+       +---+---+---+
   (2)  |.3.pull-1  |  (2)  |.3.push-7  |  (2)
        +---+---+---+       +---+---+---+
+---+---+---+---+---+---+---+---+---+---+---+---+
```

pushの意味は明解だが、pullの意味がどうも分からない(どこからのpullなのか?)。コードを読めば分かるはずだが、基本的に自分は順番を入れ替えること自体しないのでこれ以上立ち入らない(入れ替えないのであればoffsetを使えば簡単)。

さらにlessソースのレベルではデフォルトグリッド分割数(12)を始め数々の設定を自由にカスタマイズできる。ただし今回はそこまでは立ち入らない。

## Typography

TypographyはBootstrapのCSS設定の説明が主だが、ところどころclass設定の説明がある(全部まとめて一覧表にしてくれればいいのに...という訳にもいかないのだろう)。

* p.lead - パラグラフ強調(太く大きい字になる)
* .small - `<small>`の代わりに使える
* テキストアラインメント
    * .text-left - 左詰め
    * .text-center - 中央
    * .text-right - 右詰め
    * .text-justify - 均等割付(のはずだが実際は左詰め - どうも分からない)
* abbr(そう言えば使ったことない...)に表示効果を設定している
    * abbr.initialism - `<abbr>`専用オブション(全て頭文字と解釈する)
    * 例 - 小さめの大文字で'ATTR'と表示する。
        * `<abbr class='initialism' title='attribute'>attr</abbr>`

* blockquote(これは使うけど...)の中でfooterとcite(使ったことない)が効き、引用のソース情報を記述する時役立つ。

``` jade
blockquote
  p Lorem ipsum ...
  footer Someone focus in
    cite(title='Source Title') Source Title
```

```
| Lorem ipsum ...
|
| - Someone famous in Source Title
```

* blockquote.blockquote-reverseで全体が右詰めになる。

リストに関しては特記事項なし。classだけ書き残しておく。

* ul.list-unstyled - 左端の項目記号を書かない(子孫には効かない)
* ul.list-inline - 横に並べる(display: inline-blockに設定する)

Description関係の要素は自分はほぼ使ったことがないので(HTML5の最初の勉強時以来たぶん使用実績なし...)まず復習しておく。

* dl - definition list(定義リスト)、この内部にdtとdlの組を記述する
* dt - definition term(定義語)
* dd - definition descripttion(定義の説明)

構造は当然次のようになる。

``` jade
dl
  dt 用語
  dd 用語説明...
  dt 用語
  dd 用語説明...
  ...
```

普通に書いた場合の出力例。用語はboldになる。

```
用語
説明...

用語
説明...
```

dl.dl-horizontalとすると次のような表示になる(dtは右アライン)。

```
    たわば  お前はもう死んでいる...............................
            ........

  へれっつ  お前ももう死んでいる
```

dl.dl-horizontalの場合は用語(dt)が長いと適宜...で縮められる。

``` jade
dl.dl-horizontal
  dt じゅげむじゅげむごこうのすりきれかいじゃりすいぎょ...
  dd 日本一有名な長い名前
```

```
じゅげむじゅげむごこう...   日本一有名な長い名前
```

## Code

コード出力用要素のまとめ。なお内部のマークアップ文字(`&`, `<`, `>`等)は文字実体への変換が別途必要。

* code - インラインコード
* kbd - キーボード入力
* pre - preformatted text(コードブロック用)

> よく知ってるつもりだったが、実はkbd要素は今まで存在すら知らなかった...

## Tables

テーブルは実際に作って確認する。まずtableに.tableを追加することによりbootstrapの書式が有効になり、全体がフォーマットされて横線が表示される。本文と同じ表を実際に作ってみた。

``` jade
div.container
  table.table
    tbody
      tr
        th #
        th First Name
        th Last Name
        th Username
      tr
        td 1
        td Mark
        td Otto
        td @mdo
      tr
        td 2
        td Jacob
        td Thornton
        td @fat
      tr
        td 3
        td(colspan='2') Larry the Bird
        td @twitter
```

後はtableのいろいろなクラス設定で表示効果を加える。

* .table - 横幅全体にフォーマット(まずこれを指定して、以下は適宜追加)
* .table-striped - 一行おきに背景色を変える
* .table-bordered - 縦横の罫線を引く
* .table-hover - マウスをかざした行の背景色が変わる
* .table-condensed - 若干小さめになる(paddingを小さく設定する)

trやtd/thに対して次のclassを使える(背景色の設定)。

* .active - hoverした時の背景色(デフォルトは薄めのgray)
* .success - 落ち着いた感じのgreen
* .info - sky blue
* .warning - yellowとorangeの中間くらい(肌色?)
* .danger - あまりどぎつくないred

(横幅の狭い)スマホ用の対応としてtableの外側をdiv.table-responsiveで囲む。画面横幅がxsで、テーブル幅がそれより広い場合は自動的に水平スクロールバーが現れて横スクロールできるようになる。

``` jade
div.table-responsive
  table.table
    // tbody以下(略)
```

## Forms

------------------------------------------------------------------------

本題に入る前にjadeに関するワンポイント。exampleのcheckboxの部分は次のように書くとエラーになる。

``` jade
div.checkbox
  label
    // 当然これでよさそうに見えるが...
    input(type="checkbox") Check me out
```

理由はすぐ分かった。まずjadeは単独専用タグを全て認識し、例えばbrの後に何か書くとそれだけでエラーになる。

``` jade
// エラー (<br>foo</br> となってしまうので)
br foo
```

inputもbrと同じ単独専用タグ(開始と終了で挟んで中身に何かを書くということはない)なので同じ扱いというのがエラーになった理由。これにはdoctypeの問題もちょっと絡んでいる。

* XHTMLだと
    * `<input type="checkbox"><input>Check me out` と書く必要があるが
    * そういう場合はself-closing tagを使い
    * `<input type="checkbox" />Check me out` と書く
* HTML5だと
    * self closing tag自体が不要(jadeもself-closeしない)
    * `<input type="checkbox">Check me out` でよい
    * そのためjadeではいかにも`input(...) Check me out`でよさそうに見えるが
    * inputはself-closing(standalone)扱いなので中に何かを書くとエラー

解決法は次の通り。方法2は手間がかかるし、いちいちIDを定義する必要があるので以下方法1で進める。

``` jade
// 方法1 (これが自然)
label
  input(type="checkbox")
  | Check me out

// 方法2(labelとinputの順序は逆でも結果は同じ)
label(for='id-checkbox') Check me out
input#id-checkbox(type="checkbox")
```

------------------------------------------------------------------------

それでは本題のform exampleに進む。全体は次の通り。

``` jade
form(role="form")
  div.form-group
    label(for="inputEmail1") Email address
    input.form-control#inputEmail1(type="email", placeholder="Enter email")
  div.form-group
    label(for="inputPassword1") Password
    input.form-control#inputPassword1(type="password", placeholder="Password")
  div.form-group
    label(for="inputFile") File input
    input#inputFile(type="file")
    p.help-block Example block-level help text here.
  div.checkbox
    label
      input(type="checkbox")
      | Check me out
  button.btn.btn-default(type="submit") Submit
```

* .form-control - width:100%に設定(input, textarea, selectに対して有効)
    * 上では2つのinputに使っている
* (div).form-groupでlabelとinputをまとめている(上下に若干の余白ができる)
* 注意 - input groupはform-groupの中に入れること(同じレベルに置かない)
* p.help-blockは説明用ヘルプ文章(ずっと後の方に出てくる)
* div.checkboxの説明がないので調べてみた。
    * どうやらドキュメントに記述なし(grep -rもやってみたが見つからない)
    * 結局bootstrap.cssを見ると
        * これはcheckbox用の一般設定といったところ
        * 単にcheckbox全体をdiv.checkboxで囲めばいいらしい
        * 同様の設定に.radioがある(ほとんど同じ)
    * わざと外してありなしの差を比較すると、なしでは次の部分が不自然
        * checkboxとlabelの間が狭い
        * labelのテキストが太字になる

次はinline formの例。内容は同じだが横一列に配置する。

``` jade
form.form-inline(role="form")
  div.form-group
    label.sr-only(for="inputEmail2") Email address
    input.form-control#inputEmail2(type="email", placeholder="Enter email")
  div.form-group
    label.sr-only(for="inputPassword2") Password
    input.form-control#inputPassword2(type="password", placeholder="Password")
  div.checkbox
    input(type="checkbox")
    | Remember me
  button.btn.btn-default(type="submit") Sign in
```

* 基本的にはformに.form-inlineを加えるだけ
    * ただし横幅768px(sm)以上が条件(xsの横幅だと縦一列に表示する)
* inputに対応するlabelが非表示になっていることに注意
    * labelの説明はplaceholderで代用している
    * しかしlabelを消去するとscreen readerを利用している人が困ることがある
    * そこでlabel.sr-only(Screen reader only)を使っている

次はHorizontal form。これはlabelとinputの組で一列に配置するが、今度はちょっとややこしい(要grid)。

``` jade
form.form-horizontal(role="form")
  div.form-group
    label.col-sm-2.control-label(for="inputEmail3") Email
    div.col-sm-10
      input.form-control#inputEmail3(type="email", placeholder="Email")
  div.form-group
    label.col-sm-2.control-label(for="inputPassword3") Password
    div.col-sm-10
      input.form-control#inputPassword3(type="password", placeholder="Password")
  div.form-group
    div.col-sm-offset-2.col-sm-10
      div.checkbox
        label
          input(type="checkbox")
          | Remember me
  div.form-group
    div.col-sm-offset-2.col-sm-10
      button.btn.btn-default(type="submit") Sign in
```

* 先頭はform.form-horizontal
    * 指定しないと上下のinputがくっつく(labelとinputを同じ行に配置するため)
* 列合わせは.col-sm-を使って処理
    * (form.horizontal中では).form-groupは.rowの代わりにもなる
    * div.form-groupの中に2:10の比率で配置する

図解する。

```
+--------- div.form-group -------------------------+
|+---------++-------------------------------------+|
||    Email||(Email)                              ||
|+---------++-------------------------------------+|
+--------------------------------------------------+
+--------- div.form-group -------------------------+
|+---------++-------------------------------------+|
|| Password||(Password)                           ||
|+---------++-------------------------------------+|
+--------------------------------------------------+
+--------- div.form-group -------------------------+
|           +-- div.col-sm-offset-1.col-sm-10 ----+|
|           |+------div.checkbox ----------------+||
| (offset)  ||[x] Remember me                    |||
|           |+-----------------------------------+||
|           +-------------------------------------+|
+--------------------------------------------------+
+--------- div.form-group -------------------------+
|           +----- div ---------------------------+|
| (offset)  |<<Sign in>>                          ||
|           +-------------------------------------+|
+--------------------------------------------------+
|                                                  |
|<--- 2 --->|<-------------- 10 ------------------>|
```

ここで.control-labelが新しく出てきたので調査する(やはりドキュメントは若干不備が...まあ仕方ない)。

* 全文grepしたがcss/forms.html(今読んでいる部分)しかhitしない
* しかし.control-labelに関する直接の説明はない
* 仕方ないので実際にあるなしの確認を実施
    * 判別できた違いはひとつだけ(でもこれは大きな違い)
        * labelのアラインメントが違う(なしは左揃え、ありは右)
* もう少し後ろの方にvalidation stateに影響を受けるという記述がある
    * これはform用クラスのhas-\*に連動して一緒に配色が変わるという意味
    * 次のexampleを参照: 実際に色が変わっているのを確認できる
        * <http://getbootstrap.com/css/#forms-control-validation>

次は個別のフォームコントロールの解説。

最初はinput(type='...')。Bootstrapが対応しているtype一覧は次の通り。

```
text, password, datetime, datetime-local, date, month, time, week,
number, email, url, search, tel, color
```

ただしHTML5で新たに導入されたtypeはブラウザ依存が大きい。特に日時関係(date等)はFirefoxではまったく実装されていない。対応状況は調べたいブラウザで次のページを表示すると確認できる(tohoho様、いつもお世話になってます)。

<http://www.tohoho-web.com/html/input.htm>

基本的な使い方は次の通り。.form-controlによりBootstrapのlook & feelになる。またdiv.form-groupで上下のコントロールとのマージンを確保する(単独なら不要)。

``` jade
form(role="form")
  div.form-group
    input.form-control(type='text', placeholder='Text input')
```

textareaも同様(.form-groupを付ければよい)。(optionalの)rowsで最初の行数を設定できる。多くのブラウザではデフォルトは2、右下のタブで大きさを調整できる(Firefoxでは縦横両方、Chromeは縦の行数のみ)。

``` jade
  div.form-group
    textarea.form-control(placeholder='Text input', rows='3')
```

次のcheckbox/radioは2通りのレイアウトがある。まずstacked(上下に配置)の場合。

``` jade
  div.checkbox
    label
      input(type="checkbox", value="")
      | Option one is this and that&mdash;be sure to include why it's great
  div.radio
    label
      input.optionsRadios1(type="radio", name="optionsRadios", value="option1", checked)
      | Option one is this and that&mdash;be sure to include why it's great
  div.radio
    label
      input.optionsRadios1(type="radio", name="optionsRadios", value="option2")
      | Option two can be something else and selecting it will deselect option one
```

ここでは一行ごとにdiv.checkbox(または.radio)で囲っていることに注意。これで次の項目が横ではなく次の行になり、.checkboxによりチェックボックス用にマージンを確保する(.radioも同様)。

次はinline(横に並べる)。ここでのpointはlabel.checkbox-inline。同様にradioの場合は.radio-inlineを用いればよい。

``` jade
  div.form-group
    - for (var i = 1; i <= 3; ++i)
      label.checkbox-inline
        input(id = "inlineCheckbox" + i, type="checkbox", value="option" + i)
        = i
```

> 上下マージンを確保する場合は上記のようにdiv.form-groupを使う。つい間違えてdiv.checkboxとしてしまうとぐちゃぐちゃになる(.checkboxは単一のcheckboxに対して使うものなので誤り、.radioも同様)。

次のselectには直接.form-controlを設定するのがポイント。デフォルトはドロップダウン選択、multiple付きだとリストボックス風になりcontrol/shiftを使った複数項目選択を使えるようになる。

``` jade
  select.form-control
    - for (var i = 1; i <= 5; ++i)
      option= "" + i
  select.form-control(multiple)
    - for (var i = 1; i <= 5; ++i)
      option= "" + i
```

以下は間違いの例。div.form-controlで囲ってもBootstrap風にならない(divで囲まず直接select.form-controlが正解)。

``` jade
  // 誤り(Bootstrapのlook & feelにならない)
  div.form-control
    select
      - for (var i = 1; i <= 5; ++i)
        option= "" + i
```

次はform中のstatic text。`<static>`というような専用の要素はないのでp.form-control-staticを使う(次の例のemail@example.comの部分)。

``` jade
form.form-horizontal(role="form")
  div.form-group
    label.col-sm-2.control-label Email
    div.col-sm-10
      p.form-control-static email@example.com
  div.form-group
    label.col-sm-2.control-label(for="inputPassword") Password
    div.col-sm-10
      input.form-control#inputPassword(type="password", placeholder="Password")
```

Bootstrapはfocus状態のcontrol(特にinput)を(通常のoutlineを用いず)box-shadowで表現する。focusされている(入力中の)inputには空色のshadowが表示される。

> 本文中のexampleのように常にshadowが表示されることは実際はない。これはデモのため特別に表示を設定している。

disbled状態のinputは灰色表示になる。

``` jade
  div.form-group
    input.form-control#disabledInput(type="text", placeholder="Disabled input here...", disabled)
```

全体をfieldsetで囲み、fieldsetをdisabledに設定すると内部が全てdisableされる。

``` jade
form(role="form")
  fieldset(disabled)
    div.form-group
      label(for="disabledTextInput") Disabled input
      input.form-control#disabledTextInput(type="text", placeholder="Disabled input")
    div.form-group
      label(for="disabledSelect") Disabled select menu
      select.form-control#disabledSelect
        option Disabled select
    div.checkbox
      label
        input(type="checkbox")
        | Can't check this
    button.btn.btn-primary(type="submit") Submit
```

> しかしfieldset(disbled)の機能はIE9(またはより以前)で問題があり、JavaScriptを使って個別の要素をdisableするコードを書く必要がある。

Form controlにvalidation情報を表す表示効果を付けることができる。

* 親要素に次のいずれかを付ける
    * .has-warning (若干黄色っぽく...)
    * .has-error (赤っぽく...)
    * .has-success (緑っぽく...)
* その内部で次のclassを持つ要素に表示効果が適用される
    * .control-label
    * .form-control
    * .help-block

``` jade
form(role="form")
  div.form-group.has-success
    label.control-label(for="inputSuccess1") Input with success
    input.form-control#inputSuccess1(type="text")
  div.form-group.has-warning
    label.control-label(for="inputWarning1") Input with warning
    input.form-control#inputWarning1(type="text")
  div.form-group.has-error
    label.control-label(for="inputError1") Input with error
    input.form-control#inputError1(type="text")
```

これにアイコンを追加する。

``` jade
form(role="form")
  div.form-group.has-success.has-feedback
    label.control-label(for="inputSuccess2") Input with success
    input.form-control#inputSuccess2(type="text")
    span.glyphicon.glyphicon-ok.form-control-feedback
  div.form-group.has-warning.has-feedback
    label.control-label(for="inputWarning2") Input with warning
    input.form-control#inputWarning2(type="text")
    span.glyphicon.glyphicon-warning-sign.form-control-feedback
  div.form-group.has-error.has-feedback
    label.control-label(for="inputError2") Input with error
    input.form-control#inputError2(type="text")
    span.glyphicon.glyphicon-remove.form-control-feedback
```

アイコンはspan.glyphicon.glyphion-\*の形式。一覧と詳しい使い方は次の通り。

<http://getbootstrap.com/components/#glyphicons>

上の例で単にspan.glyphicon.glyphicon-okであればアイコンはinputの下に表示される(これは当然)。そこでアイコンを'feedback'してinputの右端に重ねる必要がある。 次の組合わせにより設定する。

* アイコンの親に.has-feedbackを追加
* labelは必ず必要(ないとアイコンの位置が下にずれる)
* 次がinputで...
* アイコンに.form-fontrol-feedbackを追加

パターンは次の通り。

``` jade
  //                vvvvvvvvvvvvv
  div.form-group.....has-feedback
    // labelは必須(ないとアイコンの位置ずれが発生する)
    label.control-label(for="inputSuccess2") Input with success
    input.form-control#inputSuccess2(type="text")
    //                         vvvvvvvvvvvvvvvvvvvvvv
    span.glyphicon.glyphicon-ok.form-control-feedback
```

> (以下はWarning表示メッセージより) labelなしでアイコンをinputの上に重ねたい場合はtopの値を手動で調整すれば可能。また右端位置もrightの手動調整は(一応)可能。
>
> > しかしこういうことをしていると全部その場一回限りの対応になってしまう(管理が大変)。一行しかない場合は次のようにform-horizontal扱いにすることを検討すべき。

アイコンの縦位置調整は親formのクラスにより設定を変えている。

* オプションclassなしのformはlabelがあると仮定して計算
* form.horizontalまたは.inlineはlabelなし(または同じ行にある)として計算

horizontalとinlineの例。どちらも実際に確認した。

``` jade
form.form-horizontal(role="form")
  div.form-group.has-success.has-feedback
    label.control-label.col-sm-3(for="inputSuccess3") Input with success
    div.col-sm-9
      input.form-control#inputSuccess3(type="text")
      span.glyphicon.glyphicon-ok.form-control-feedback

form.form-inline(role="form")
  div.form-group.has-success.has-feedback
    label.control-label(for="inputSuccess4") Input with success
    input.form-control#inputSuccess4(type="text")
    span.glyphicon.glyphicon-ok.form-control-feedback
```

コントロールの高さは3通りから設定できる。

* .input-lg - 通常より高く(大きく)
* なし(デフォルト) - 通常の高さ
* .input-sm - 通常より低く(小さく)

> CSSソースをgrepしたが.input-mdや.input-xsはない。

``` jade
form(role="form")
  input.form-control.input-lg(type="text", placeholder=".input-lg")
  input.form-control(type="text", placeholder="Default input")
  input.form-control.input-sm(type="text", placeholder=".input-sm")
  select.form-control.input-lg
    option .input-lg
  select.form-control
    option Default input
  select.form-control.input-sm
    option .input-sm
```

横幅調整はgridを使う。

* 外側にdiv.rowの囲いを作る(以下次の微妙な点があるので注意)
    * form.form-horizontalの場合はdiv.form-groupでもOK(たぶんbetter)
    * しかし普通のformでdiv.form-groupを使うと
        * 内部分割はされるが...
        * その次の要素の配置がおかしい(具体的には改行しない)
* 内部をdiv.col-xx-xで配置/分割
    * その中にcontrolを入れる

``` jade
form(role="form")
  div.row
    div.col-xs-2
      input.form-control(type="text", placeholder=".col-xs-2")
    div.col-xs-3
      input.form-control(type="text", placeholder=".col-xs-3")
    div.col-xs-4
      input.form-control(type="text", placeholder=".col-xs-4")
```

> 直接input.form-control.col-xs-2...などと直接設定したくなるがそれは無理(.form-controlは幅一杯に取る設定なので相容れない)。そこでdiv.col-xs-2の箱を作りその中に入れる。

説明用テキストは.help-blockを使う。p.help-blockはformの最初のexampleに出てきている。ここではspan.help-blockを使っているが表示に変わりはない。

``` jade
  div.form-group
    input.form-control#inputEmail1(type="text")
    span.help-block A block of help text that breaks onto a new line and may extend beyond one line.
```

## Buttons

ボタンの設定。

* button.btn - まずこれが必須
    * .btn-default (白)
    * .btn-primary (青)
    * .btn-success (緑)
    * .btn-info (水色)
    * .btn-warning (オレンジ)
    * .btn-danger (赤)
    * .btn-link (白、枠なし)

``` jade
form(role="form")
  button.btn.btn-default(type="button") Default
  button.btn.btn-primary(type="button") Primary
  button.btn.btn-success(type="button") Success
  button.btn.btn-info(type="button") Info
  button.btn.btn-warning(type="button") Warning
  button.btn.btn-danger(type="button") Danger
  button.btn.btn-link(type="button") Link
```

サイズは4種類ある。

* .btn-lg - Large
* (なし) - Default
* .btn-sm - Small
* .btn-xs - Extra Small

> .btn-mdはない(grepして確かめた)。

``` jade
form(role="form")
  p
    button.btn.btn-primary.btn-lg(type="button") Large
    button.btn.btn-default.btn-lg(type="button") Large
  p
    button.btn.btn-primary(type="button") Default
    button.btn.btn-default(type="button") Default
  p
    button.btn.btn-primary.btn-sm(type="button") Small
    button.btn.btn-default.btn-sm(type="button") Small
  p
    button.btn.btn-primary.btn-xs(type="button") Xtra Small
    button.btn.btn-default.btn-xs(type="button") Xtra Small
```

buttonはデフォルトでinlineだが、.btn-blockを用いればblock要素にできる。

``` jade
form(role="form")
  div.row
    div.col-md-offset-3.col-md-6
      button.btn.btn-primary.btn-block(type="button") Block level button
      button.btn.btn-default.btn-block(type="button") Block level button
```

その次はコントロール要素のactive状態制御に関する説明。どうもよく分からないので一応文章だけまとめておく。

* ボタンは(押下中に発生する):active擬似クラスを用いて描画制御している
* `<a>`要素は.activeを用いる
* ボタンの場合もJavaScriptで(イベントを捉えて).activeで処理することも可

> (後で追加) buttonのようなcontrolの表示設定は擬似クラスの:hover(マウスをかざす)と:active(クリック)を使う。本来擬似クラスは自分では勝手に制御できないが、クリックした状態を再現したい場合のために.activeを用意している。

実際にexampleで確認する。.activeを付けると表示が常に押しっぱなし状態のボタンになる(ただし表示効果を細工しているだけで実際のクリックとは無関係)。比較のため.activeなしのボタンも一緒に表示した。

``` jade
form(role="form")
  div.form-group
    p.help-block Normal
    button.btn.btn-primary(type="button") Primary button
    button.btn.btn-default(type="button") Button
  div.form-group
    p.help-block Active (pressed)
    button.btn.btn-primary.active(type="button") Primary button
    button.btn.btn-default.active(type="button") Button
```

`<a>`要素に.btn.btn-\*を加えるとボタンと同じ表示になる。この場合も.activeは同じように働き、押したままのように描画される。

``` jade
form(role="form")
  div.form-group
    p.help-block Normal
    a.btn.btn-primary(href='#', role="button") Primary link
    a.btn.btn-default(href='#', role="button") Link
  div.form-group
    p.help-block Active
    a.btn.btn-primary.active(href='#', role="button") Primary link
    a.btn.btn-default.active(href='#', role="button") Link
```

> buttonとaで異なる点はマージンで、buttonを2つ横に並べると間に隙間ができるが、aを並べると密着する。
> 
> > ちなみにaに対するrole="button"はaccessibility対応だが、この場合はボタン形状になっているだけでaの機能が変わる訳ではない。自分は不要だと思う。

ボタンにdisabled属性を加えると半分(50%)の薄さにして表示する。

``` jade
form(role="form")
  div.form-group
    p.help-block Normal
    button.btn.btn-primary(type="button") Primary button
    button.btn.btn-default(type="button") Button
  div.form-group
    p.help-block Disabled
    button.btn.btn-primary(type="button", disabled) Primary button
    button.btn.btn-default(type="button", disabled) Button
```

> IE9はbutton(disable)の表示に特徴(?)があり、強制的に(本文によれば'nasty'な)影付きテキストで表示する(下記URL参照)。これはどうやっても直せないそうだ。
> 
> <http://stackoverflow.com/questions/8766987/css-remove-shadows-on-disabled-html-buttons>

a要素の場合は(disabled属性はないので).disabledを使う。

``` jade
form(role="form")
  div.form-group
    p.help-block Normal
    a.btn.btn-primary(href='#', role="button") Primary link
    a.btn.btn-default(href='#', role="button") Link
  div.form-group
    p.help-block Disabled
    a.btn.btn-primary.disabled(href='#', role="button") Primary link
    a.btn.btn-default.disabled(href='#', role="button") Link
```

Bootstrapのボタン系クラスが使えるタグは次の通り。

* button - これは当然として
* input - HTML4以前の方法(type='submit'または'button', 'reset')
* a - Bootstrap特有の機能

> aをボタンと同じ表示にできるとボタンに直接リンクを貼れるので、昔はJavaScriptプログラミングが必要だった処理をstatic HTMLだけで済ますことができる(これはよいアイデア)。

``` jade
form(role="form")
  a.btn.btn-default(href="#", role="button") Link
  button.btn.btn-default(type="submit") Button
  input.btn.btn-default(type="button", value="Input")
  input.btn.btn-default(type="submit", value="Submit")
```

> Cross-browser issueとして、極力(input type='submit'等ではなく)buttonを使うようにと書いてある(Firefoxのバグ回避のため)。

## Images

最後はimg要素。.img-responsibleを付けると巨大な画像を画面に入るよう適宜調整してくれる。ちょうどいい大きさのtwitterロゴ画像を見つけたので使ってみた。

``` jade
img.img-responsive(src="https://g.twimg.com/Twitter_logo_blue.png", alt="Responsive image")
```

表示効果の補助クラスがある。

* .img-rounded - 角を丸める
* .img-circle - 円でくり抜く
* .img-thumbnail - 周囲に枠を付ける(サムネール用)

今度はWikipediaにある有名なアルバムジャケットを使う(正方形なので効果が分かりやすい)。

``` jade
div.container
  - var url = "http://upload.wikimedia.org/wikipedia/en/3/3b/Dark_Side_of_the_Moon.png"
  img(src=url)
  img.img-rounded(src=url)
  img.img-circle(src=url)
  img.img-thumbnail(src=url)
```

以上で個別の要素に対する解説は終了。

## Helper Classes

テキスト汎用の補助クラス。

* .text-muted (50% gray)
* .text-primary (以下はボタンの色と同じなので説明略)
* .text-success
* .text-info
* .text-warning
* .text-danger

背景用の補助クラス。これもボタンの色と同じなので説明略。

* .bg-primary
* .bg-success
* .bg-info
* .bg-warning
* .bg-danger

次の例はclose icon(`&times;`は掛け算マーク)の表示だが、この説明を読んでも何を言いたいのか分からない("like modals and alerts"と書いてあるが...)。

``` jade
button.close(type="button", aria-hidden="true") &times;
```

> aria-hiddenはaccessibility用の新しい属性。次を参照。
> 
> <http://www.w3.org/TR/wai-aria/states_and_properties#aria-hidden>
> 
> 解説を見つけた。基本勉強で一杯一杯の状況ではここまで対応する余裕はないだろう。でも頭のどこかに留めておくことにする。
> 
> <http://memolog.org/2012/05/aria-hidden.html>

------------------------------------------------------------------------

(以下しばらく参考: 試行錯誤過程の記録だが、分かってみたら馬鹿みたいだった...) 意味が分からなかったので.closeの効果を確認してみた。

``` jade
// 実は文字は何でもいい
div
  p.close あ
    span.close あ
```

結果をまとめる。

* .closeを付けると...次はCSSコードの予想
    * display: inline
    * text-align: right
    * font-weight: bold
    * (おそらく半分程度の)grayed
        * 上の例では入れ子になっているため内側のspanは25%表示になる
    * pull-rightする

実際にソースを見たら大体合っていた。なおgrayedの入れ子は次のようにfilterで処理しているが、opacitryの設定に若干ずれがあった(デフォルトのcontrastが最大に設定されているため1/2よりも弱くしている)。

``` jade
// ソースより

// 通常状態 - 白地100%に黒文字100%なので50%では濃すぎるということ
filter: alpha(opacity=20);

// マウスをかざした時(感覚的にはこれくらいかな...)
filter: alpha(opacity=50);
```

とにかく.closeの効果は分かった。バツ印を想定したものなので.closeという名前になっているが、実際は何にでも使える。

------------------------------------------------------------------------

後でComponentsの最後の方を読んで意味が分かった。これは単にdismissable alertやmodalを閉じるためのチェックボタンに用いる表示効果設定だった(こんなに詳しく調べる必要はなかった)。

> Dismissable alertの例は次を参照。Exampleの右端のcloseボタン(X)をクリックするとalertが閉じる(消滅する)のを確認できる。
> 
> <http://getbootstrap.com/components/#alerts-dismissable>
> 
> Modalは次を参照。Exampleは2つあり、最初の例は画面の作り方の説明(closeしない)。後半に実際にmodal動作するLive exampleがある(要JavaScript)。
> 
> <http://getbootstrap.com/javascript/#modals-examples>

次は下向き三角印の.caret(ドロップダウンメニューに使う)。

``` jade
span.caret
```

> この先CSSのところどころで`!important`という設定が出てくる。これは「(この後で同じ設定が上書きされても)これが最優先(キャンセルされない)」という意味。次の説明を参照。
> 
> <http://www.htmq.com/csskihon/007.shtml>

要素を左右に寄せてfloatさせる。

* .pull-left
* .pull-right

``` jade
// spanでも同じ
div.pull-left X
div.pull-right Y
| あいうえお
```

次のように表示する。

```
Xあいうえお                                      Y
```

> navbar用には専用の.navbar-leftと.navbar-rightを使う。

ブロック単位中央寄せは.center-blockと書いてあるようだが...機能しない。

``` jade
// 中央に来ない
div.center-block あいうえお
```

issueを見つけたので記録しておく。開発者には何か意図があるようだ。

<https://github.com/twbs/bootstrap/issues/11771>

コードは次の通り(たったこれだけ)。左右のマージンを均等にするというだけの意味らしい。

``` css
.center-block {
  display: block;
  margin-right: auto;
  margin-left: auto;
}
```

次の.clearfixはgridの方ですでに詳しく説明しているのでそちらを参照(ここでは略)。

表示/非表示設定は次を使う。

* .show - これは文字通りの意味
* .hidden - screen reader非使用時は表示しない(レイアウトもしない)
* .invisible - 表示はしないがレイアウトはする(スペースが空く)

> .hideもある(screen readerと無関係に隠す)。しかし.hideはdeprecated扱いで、.hiddenを使うか、または.sr-onlyと組み合わせての使用を推奨している。

次はaccessibility用の設定。もう何回か出てきているが復習する。

* .sr-only - screen reader使用時だけ表示

次の.text-hideは次のように使う(これもaccessibility対応の一種)。

``` jade
// 文字は表示されないが行は空く
// (background-imageで同じ文字をかっこいいフォントで表示するような場合)
h1.text-hide#custom-heading Custom heading
```

CSS側の例。

``` css
/* たぶんこんな感じ(未確認) */
#custom-heading {
  background-image: url(../image/custom-heading.png);
}
```

## Responsive utilities

次の表示/非表示制御は現在の実装ではblockとtableに対してのみ有効(table内の要素には効かない)。

```
                xtra-small  small       medium      large
--------------  ----------  ----------  ----------  ----------
.visible-xs     visible     hidden      hidden      hidden
.visible-sm     hidden      visible     hidden      hidden
.visible-md     hidden      hidden      visible     hidden
.visible-lg     hidden      hidden      hidden      visible
.hidden-xs      hidden      visible     visible     visible
.hidden-sm      visible     hidden      visible     visible
.hidden-md      visible     visible     hidden      visible
.hidden-lg      visible     visible     visible     hidden
```

次はscreen(browser)とprintのデバイスに対する表示/非表示設定。

```
                browser     print
--------------  ----------  ----------
.visible-print  hidden      visible
.hidden-print   visible     hidden
```

次のTest casesはリンクを示す(ソースはかなり長いので略)。実際に画面の横幅を変化させてこの部分のページの表示変化を試してみることができる(ボタンが現れたり消えたりする)。

<http://getbootstrap.com/css/#responsive-utilities-tests>

次のUsing LessやUsing Sassは略(もし後でカスタマイズすることがあったら読む)。

それでは次のComponentsに進む(いやけっこう長かった)。


Components
========================================================================
<http://getbootstrap.com/components/>

## Glyphicons

使い方の例。

``` jade
span.glyphicon.glyphicon-thumbs-up
|  いいね!
```

Exampleとほぼ同じものを作ってみた(.btn-groupと.btn-toolbarは後で出てくるがその予習も兼ねる)。

``` jade
div.btn-toolbar
  div.btn-group
    - var alignments = ['left', 'center', 'right', 'justify']
    - for (var i = 0; i < alignments.length; ++i)
      button.btn.btn-default
        span(class = 'glyphicon glyphicon-align-' + alignments[i])
div.btn-toolbar
  - var sizes = [' btn-lg', '', ' btn-sm', ' btn-xs']
  - for (var i = 0; i < sizes.length; ++i)
    button(class = 'btn btn-default' + sizes[i])
      span.glyphicon.glyphicon-star
      |  Star
```

## Dropdowns

Dropdownを使うにはまずJavaScriptのbootstrap(.min).jsが必要。このセットアップはすでにできているのでまずはexampleを試してみる。しかし動かない...

``` jade
div.dropdown
  button.btn.dropdown-toggle.sr-only#dropdownMenu1(type="button", data-toggle="dropdown") Dropdown 
    span.caret
  ul.dropdown-menu(role="menu", aria-labelledby="dropdownMenu1")
    li(role="presentation")
      a(role="menuitem", tabindex="-1", href="#") Action
    li(role="presentation")
      a(role="menuitem", tabindex="-1", href="#") Another action
    li(role="presentation")
      a(role="menuitem", tabindex="-1", href="#") Something else here
    li.divider(role="presentation")
    li(role="presentation")
      a(role="menuitem", tabindex="-1", href="#") Separated link
```

> 以下はトラブルシューティング記録。ソースはドキュメントのexampleと(ちゃんとは確認してないがたぶん)等価だが、ドキュメント内では動くのに別の場所では動かないというところにヒントがあった。

ちょっと悩んだが.sr-onlyを外すと動く。ここから状況を把握できた。実はbuttonの部分に誤りがあり、次のように書くのが正しいらしい(button全体に.sr-onlyがかかると全体が非表示になってしまう)。

``` jade
  // このように修正すれば動く(.sr-onlyを完全消去)
  // 行末(Dropdownの後)にスペース1つが必要(ないとcaretと密着する)
  button.btn.dropdown-toggle#dropdownMenu1(type="button", data-toggle="dropdown") Dropdown 
    span.caret
```

> ドキュメントではメニューを出したままにする追加処理をしている(詳細は未確認だがまず間違いない)。その際.sr-onlyを利用してメニューボタン全体を消しているが、これを(修正せず)そのままコードリスティングに貼ってしまったようだ。

それでは解析する。

* 外枠はdiv.dropdown(これしか説明してない)、内部は次の通り
    * button.btn.dropdown-toggle#id(type="button", data-toggle="dropdown")
        * .btnはBootstrapの表示にするため(機能上は不要)
        * .dropdown-toggleはお決まりらしい
            * dropdownするものには必ず付けている
            * ただし表示効果だけなのでなくても機能はする
            * しかしこの場合は外してみてもどうも効果の違いが分からない
        * #idはその先のulからの参照用
            * しかし...なくても動く...
        * type="button"はあったほうが丁寧(デフォルトはsubmitのため)
            * しかしどうせJavaScriptでイベント処理しているためほぼ無関係
        * data-toggle="dropdown"の部分が必須(削除すると動かない)
            * data-toggleはHTML仕様にはない属性
            * bootstrap.jsを読むとクリック時アクションの判定に使っている
                * data-toggle="dropdown"でドロップダウンメニュー
                * 他に"button", "modal", "tab"など多数(後で出てくる)
    * ul.dropdown-menu(role="menu", aria-labelledby="[id]")
        * これでメニュー項目を表現
        * .dropdown-menuは必須(付けないと普通のulとして処理する)
        * role="menu" はaccessibility用(外しても動作は変わらない)
            * 理由はulをリストではなくメニューに流用しているため
        * aria-labelledby="[id]" も今では不要みたい
            * JavaScriptソースを検索したが見つからない
            * たぶん以前はこれで参照していたのだろう(昔はあったはず)
            * JavaScriptコードの改良により不要になったのでは?
    * liの書式は次の通り
        * li(role="presentation") CONTENT
            * やはりroleは省略可
        * CONTENTの中にaを書く場合の例は次の通り
            * a(role="menuitem", tabindex="-1", href="#") Action
            * roleは省略可
            * tabindexはTABキーによるフォーカス移動順位だが、これも省略可
                * JavaScriptソースを見ても使っている形跡なし
                * 後ろの方のexampleにはtabindexはもう書いてない
                * よって不要と判断する
            * hrefはもちろん普通に機能する
        * li.dividerはその名の通り

> aria-という接頭辞は本ドキュメントの後半やJavaScriptソースの所々に出てくる。ariaは音楽のアリアのことなので何か意味があるのだろう(さすがにareaのスペルミスではないはず...)。

> > そう言えば前にaria-hiddenというのがあった...とここで思い出した。WAI-ARIAというのはaccessibility用にW3Cが提案している仕様。次を参照。
> > 
> > http://www.w3.org/WAI/PF/aria/

いやこれはちょっと大変だった。まとめてみる。

* 機能上必須なのは次の3つ
    * div.dropdown
    * button(data-toggle="dropdown")のdata-toggle属性
    * ul.dropdown-menu
* 表示効果で必要なclass設定
    * button.btn.dropdown-toggle
    * li.divider
* 今では不要と思われるもの(作る人と書く人は別なのである程度仕方ない)
    * buttonのid
    * aria-labelled-by="[id]"
    * tabindex="-1"
* roleを用いる理由はulやliなどを本来のタグの意味とは別目的に使っているため
    * accessibility対応なのでなくても動く
    * 自分なら開発当初は全て省略して、リリース時に全部まとめて対応する

最低限の設定は次の通り。これで問題なく動く。

``` jade
div.dropdown
  button.btn.dropdown-toggle(type="button", data-toggle="dropdown") Dropdown 
    span.caret
  ul.dropdown-menu
    li: a(href="#") Action
    li: a(href="#") Another action
    li: a(href="#") Something else here
    li.divider
    li: a(href="#") Separated link
```

> ul.dropdown-menu.dropdown-menu-right とすると画面右端にdropdownする。

これで全て把握できたので次の2つを加える。dropdownは以上で終わり。

* Headers (li.dropdown-header)
* Disabled item (li.disabled)

``` jade
div.dropdown
  button.btn.dropdown-toggle(type="button", data-toggle="dropdown") Dropdown 
    span.caret
  ul.dropdown-menu
    li.dropdown-header Dropdown header
    li: a(href="#") Action
    li.disabled: a(href="#") Disabled
    li: a(href="#") Something else here
    li.divider
    li.dropdown-header Dropdown header
    li: a(href="#") Separated link
```

> 以下roleやaria-\*などのaccessibility用属性は学習時間短縮のため適宜省略し、将来成果物を公開する時期になったらその時点で調べて一括対応する。

## Button groups

ボタングループを作るとボタンが密着し、全体を角丸の枠で囲んで表示する。

* 外枠としてdiv.btn-groupで囲む

``` jade
div.btn-group
  - var items = ["Left", "Middle", "Right"]
  - for (var i = 0; i < items.length; ++i)
    button.btn.btn-default(type='button')= items[i]
```

複数のボタングループを横につなげてツールバーにする。

* 全体をdiv.btn-toolbarで囲む

``` jade
div.btn-toolbar
  div.btn-group
    - for (var i = 1; i <= 4; ++i)
      button.btn.btn-default(type='button')= i
  div.btn-group
    - for (var i = 5; i <= 7; ++i)
      button.btn.btn-default(type='button')= i
  div.btn-group
    button.btn.btn-default(type='button') 8
```

サイズ設定はボタン個別ではなくグループに対して行う。

* btn-group-lg
* (mdはデフォルト値のためなし)
* btn-group-sm
* btn-group-xs

``` jade
- var sizes = ['lg', null, 'sm', 'xs']
- var items = ['Left', 'Center', 'Right']
- for (var sz = 0; sz < sizes.length; ++sz)
  div.btn-toolbar
    - var klass = 'btn-group'
    - if (sizes[sz]) klass += ' btn-group-' + sizes[sz]
    div(class=klass)
      - for (var i = 0; i < items.length; ++i)
        button.btn.btn-default(type='button')= items[i]
```

ボタングループの中にドロップダウンメニューを入れる場合は(div.dropdownの代わりに)div.btn-groupを使う(nestする)。

``` jade
div.btn-group
  - for (var i = 1; i <= 2; ++i)
    button.btn.btn-default(type='button')= i
  div.btn-group
    button.btn.btn-default.dropdown-toggle(type='button', data-toggle='dropdown') Dropdown 
      span.caret
    ul.dropdown-menu
      - for (var j = 1; j <= 2; ++j)
        li: a(href='#') Dropdown link
```

縦に配置する場合はdiv.btn-group-verticalを指定する。

> (次のsectionの)Split button dropdownには使えない。

Exampleと同じものを実際に作ってみた。

``` jade
div.btn-group-vertical
  - for (var i = 1; i <= 2; ++i)
    button.btn.btn-default(type='button') Button
  div.btn-group
    button.btn.btn-default.dropdown-toggle(type='button', data-toggle='dropdown') Dropdown 
      span.caret
    ul.dropdown-menu
      - for (var j = 1; j <= 2; ++j)
        li: a(href='#') Dropdown link
  - for (var i = 1; i <= 2; ++i)
    button.btn.btn-default(type='button') Button
  - for (var i = 0; i < 3; ++i)
    div.btn-group
      button.btn.btn-default.dropdown-toggle(type='button', data-toggle='dropdown') Dropdown 
        span.caret
      ul.dropdown-menu
        - for (var j = 1; j <= 2; ++j)
          li: a(href='#') Dropdown link
```

(横幅いっぱいに)justifiedしたボタングループの作成法は次の通り。

* 外枠のdiv.btn-groupに.btn-group-justifiedを追加
* aを使う場合はこれだけでOK
* buttonを使う場合は内側にdiv.btn-groupを作りbuttonをその中に入れる
    * これは一部のブラウザがjustificationを正しく処理しない事に対する対策

``` jade
- var items = ['Left', 'Center', 'Right']

// aを使う場合
div.btn-group.btn-group-justified
  - for (var i = 0; i < items.length; ++i)
    a.btn.btn-default= items[i]

// buttonを使う場合
div.btn-group.btn-group-justified
  - for (var i = 0; i < items.length; ++i)
    // ここにもう一段必要
    div.btn-group
      button.btn.btn-default(type='button')= items[i]
```

## Button dropdowns

ボタンの中にメニューを入れる方法はすでに出てきたが復習する。

* 外枠としてdiv.btn-groupを作り(div.dropdownの代わり)
* その中にbuttonとulを入れる。

Exampleを作ってみた(やはりjadeだと早い)。

``` jade
- var types = ['Default', 'Primary', 'Success', 'Info', 'Warning', 'Danger']
- for (var i = 0; i < types.length; ++i)
    div.btn-group
      - var klass = 'dropdown-toggle btn btn-' + types[i].toLowerCase()
      button(class=klass, type='button', data-toggle='dropdown')
        = types[i] + ' '
        span.caret
      ul.dropdown-menu
        li: a(href='#') Action
        li: a(href='#') Another Action
        li: a(href='#') Something else here
        li.divider
        li: a(href='#') Separated link
```

Splitする場合は次の通り。実は2個のbuttonの組でできている。

* 外枠div.btn-groupの中に次の3つを入れる
    * 最初のbutton.btnにはdata-toggle属性を指定しない(普通のボタン)
    * 次のbutton.btnにdata-toggle='dropdown'を設定(ここがメニュー)
        * 内部にspan.carotを入れる
    * 最後はul.dropdown-menu

これもexampleと同じものを作ってみた。

``` jade
- var types = ['Default', 'Primary', 'Success', 'Info', 'Warning', 'Danger']
- for (var i = 0; i < types.length; ++i)
    div.btn-group
      - var klass = 'btn btn-' + types[i].toLowerCase()
      button(class=klass, type='button')= types[i]
      button(class=klass + ' dropdown-toggle', type='button', data-toggle='dropdown')
        span.caret
      ul.dropdown-menu
        li: a(href='#') Action
        li: a(href='#') Another Action
        li: a(href='#') Something else here
        li.divider
        li: a(href='#') Separated link
```

サイズは4種類設定できる(CSSのセクションですでに学んでいるが復習)。

* .btn-lg - Large
* (なし) - Default
* .btn-sm - Small
* .btn-xs - Extra Small

``` jade
- var sizes = ['lg', null, 'sm', 'xs']
- var faces = ['Large', 'Medium', 'Small', 'Extra small']
- for (var i = 0; i < sizes.length; ++i)
    div.btn-group
      - var klass = 'btn btn-default dropdown-toggle'
      - if (sizes[i]) klass += ' btn-' + sizes[i]
      button(class=klass, type='button', data-toggle='dropdown')
        = faces[i] + ' '
        span.caret
      ul.dropdown-menu
        li: a(href='#') Action
        li: a(href='#') Another Action
        li: a(href='#') Something else here
        li.divider
        li: a(href='#') Separated link
```

上向きにdrop-upするメニューも作れる。

* 外枠のdiv.btn-groupに.dropupを追加
* デフォルトではメニューはボタン左端にalign (.pull-left)
* ボタン右端にalignする場合はul.dropdown-menuに.pull-rightを追加

Exampleはsplit buttonだが、ここはあえてsplitなしで作ってみた。

``` jade
- var settings = [{type:'default', face:'Dropup', pull:'left' }, {type:'primary', face:'Right dropup', pull:'right'}]
- for (var i = 0; i < settings.length; ++i)
    div.btn-group.dropup
      - var klass = 'dropdown-toggle btn btn-' + settings[i].type
      button(class=klass, type='button', data-toggle='dropdown')
        = settings[i].face + ' '
        span.caret
      ul(class = 'dropdown-menu pull-' + settings[i].pull)
        li: a(href='#') Action
        li: a(href='#') Another Action
        li: a(href='#') Something else here
        li.divider
        li: a(href='#') Separated link
```

## Input groups

まずは最初の例を試してみる。

* div.input-groupが外枠
* input.form-control(type='text')が一行入力の本体
* span.input-group-addonで補助テキスト(addon)を前後に配置できる

``` jade
// 手前に配置
div.input-group
  span.input-group-addon @
  input.form-control(type="text", placeholder="Username")
br
// 末尾に配置
div.input-group
  input.form-control(type="text")
  span.input-group-addon .00
br
// 前後両方に配置
div.input-group
  span.input-group-addon $
  input.form-control(type="text")
  span.input-group-addon .00
```

> brはコードリスティングには書かれていないが、実際のexampleで使われている(Chrome devtoolsで確認 - これがないと上下が密着する)。

サイズ設定。

* div.input-groupに次の設定を追加できる(3通り - extra smallはない)
    * input-group-lg - Large
    * (なし) - Medium
    * input-group-sm - Small

``` jade
- var sizes = ['lg', null, 'sm']
- for (var i = 0; i < sizes.length; ++i)
  - var klass = 'input-group'
  - if (sizes[i]) klass += ' input-group-' + sizes[i]
  div(class=klass)
    span.input-group-addon @
    input.form-control(type="text", placeholder="Username")
  br
```

Addonの部分にcheckbox/radioを使うことができる。

``` jade
- var types = ['checkbox', 'radio', 'radio', 'radio']
- for (var i = 0; i < types.length; ++i)
  div.row
    div.col-lg-6
      div.input-group
        span.input-group-addon
          input(type=types[i], name= types[i] == 'radio' ? 'radio1' : "", checked = i == 2)
        input.form-control(type="text")
    - if (types[i] == 'checkbox')
      br
```

> Radio用設定を追加した。
> 
> * radioを3つに増やしgroupingにname属性を設定(これで実際のradio動作になる)
> * checked={boolean}で初期値設定

次はaddonの部分にボタンを配置する例。

* (.input-group-addonではなく).input-group-button(初めて出てきた)
    * その内部にbuttonを入れる

``` jade
div.row
  div.col-lg-6
    div.input-group
      // div.input-group-btn でも同じ(exampleはdivにしている)
      span.input-group-btn
        button.btn.btn-default(type="button") Go!
      input.form-control(type="text")
  div.col-lg-6
    div.input-group
      input.form-control(type="text")
      span.input-group-btn
        button.btn.btn-default(type="button") Go!
```

> lg幅の場合だけ横に並べて配置、それより小さいと上下に配置する。ただしexampleでは上下が密着せずマージンが付くがこの理由はまだ不明(自分で同じ事をすると密着する)。この場合はbrは入れられない(lgの場合に横に並ばない)。

さらにボタンの中にdropdownを挿入する。

``` jade
// これはさすがに大変なので片方だけ
div.input-group
  span.input-group-btn
    button.btn.btn-default.dropdown-toggle(type="button", data-toggle="dropdown")
      | Action
      span.caret
    ul.dropdown-menu
      li: a(a href="#") Action
      li: a(a href="#") Another action
      li: a(a href="#") Something else here
      li.divider
      li: a(a href="#") Separated link
  input.form-control(type="text")
```

Segmented buttonの例。

* まず全体の枠はdiv.input.group
    * (split用のdiv.btn-groupの代わりに)div.input-group-btnで囲み
        * 普通のボタン
        * data-toggle='dropdown'属性付きボタン(クリックでメニュー表示)
        * メニューアイテム用のul.dropdown-menu
    * input.form-fontrol(type='text')

``` jade
// これも片方だけ
form(role='form')
  div.input-group
    div.input-group-btn
      button.btn.btn-default(type='button') Action
      button.btn.btn-default.dropdown-toggle(type="button", data-toggle="dropdown")
        span.caret
      ul.dropdown-menu
        li: a(a href="#") action
        li: a(a href="#") another action
        li: a(a href="#") something else here
        li.divider
        li: a(a href="#") separated link
    input.form-control(type="text")
```

## Navs

タブコントロールは2種類用意してある。本sectionのコントロールは常にベースクラス.navが付く。

> ただしこれだけでは自動的に切り替わってはくれない(static page用)。もう少し手を加えればdynamicにできる。次を参照(JavaScriptコードを書かなくてもできる: Markupの部分を読むこと)。
> 
> http://getbootstrap.com/javascript/#tabs

* ul.nav.nav-tabs
* ul.nav.nav-pills
    * どちらも内側にliを書く
    * li.active が「選択項目」(pill表示の場合primaryの色になる)
    * li.disabledにするとgrayed表示
        * でも実際にやってみるとクリックは受け付ける
    * liの内側にはさらにa(href='#') Textが必要
* 縦に配置する場合は.nav-stackedを追加
    * ただし使えそうなのはpillsだけ(tabも可能だが使える表示効果ではない)
* 横一杯に配置するには.nav-justifiedを追加

``` jade
// tabsの例
ul.nav.nav-tabs
  li.active: a(href='#') Home
  li: a(href='#') Profile
  li: a(href='#') Messages

// 縦配置pillsの例
div.row
  // これくらいの幅が適当か?
  div.col-sm-4
    ul.nav.nav-pills.nav-stacked
      li: a(href='#') Home
      li.active: a(href='#') Profile
      li: a(href='#') Messages

// justifiedの例(disabled付き)
ul.nav.nav-tabs.nav-justified
  li.active: a(href='#') Home
  li: a(href='#') Profile
  li: a(href='#') Messages
  li.disabled: a(href='#') Disabled link
```

中にdropdownを入れる。

* liに.dropdownを追加
    * `a.dropdown-toggle(href='#', data-toggle='dropdown')`が決まり文句
        * .dropdown-toggleはクリックでdropdownする要素共通のCSS表示効果
        * href='#'がないと(機能はするが)マウスポインタがI-beamになってしまう
        * data-toggle='dropdown'はJavaScript用に必須
    * その後はul.dropdown-menu

``` jade
// tabs/pillsとも同じなので片方だけ
ul.nav.nav-tabs
  li.active: a(href='#') Home
  li: a(href='#') Help
  li.dropdown
    // 次の一行はこの場合の必須パターン(全て必要)
    a.dropdown-toggle(href='#', data-toggle='dropdown')
      | Dropdown 
      span.caret
    ul.dropdown-menu
      li: a(a href="#") Action
      li: a(a href="#") Another action
      li: a(a href="#") Something else here
      li.divider
      li: a(a href="#") Separated link
```

## Navbar

おそらくここが最難関。まず最初のexampleはかなり長いがちゃんと試してみる。

> (後で分かったが)本文には十分な説明はない。自力で解析しないと理解できない。

冒頭の説明でNavbarは"resiponsive"なmeta componentという記述があることに注意。このexample navbarは幅を狭めていくとある時点(xs境界付近)でバーが'collapse'してモバイル仕様の縦メニューに切り替わる。

``` jade
// jadeでもこんなに長いとちょっと大変だが...ここは手抜きしてはいけない
nav.nav.navbar-default
  div.container-fluid
    div.navbar-header
      button.navbar-toggle(type="button", data-toggle="collapse", data-target="#bs-example-navbar-collapse-1")
        span.sr-only Toggle navigation
        - for (var i = 0; i < 3; ++i)
          span.icon-bar
      a.navbar-brand(href="#") Brand
    div.collapse.navbar-collapse#bs-example-navbar-collapse-1
      ul.nav.navbar-nav
        li.active: a(href="#") Link
        li: a(href="#") Link
        li.dropdown
          a.dropdown-toggle(href="#", data-toggle="dropdown")
            | Dropdown 
            b.caret
          ul.dropdown-menu
            li: a(href="#") Action
            li: a(href="#") Another action
            li: a(href="#") Something else here
            li.divider
            li: a(href="#") Separated link
            li.divider
            li: a(href="#") One more separated link
      form.navbar-form.navbar-left(role="search")
        div.form-group
          input.form-control(type="text", placeholder="Search")
        button.btn.btn-default(type="submit") Submit
      ul.nav.navbar-nav.navbar-right
        li: a(href="#") Link
        li.dropdown
          a.dropdown-toggle(href='#', data-toggle='dropdown')
            | Dropdown 
            b.caret
        ul.dropdown-menu
          li: a(a href="#") Action
          li: a(a href="#") Another action
          li: a(a href="#") Something else here
          li.divider
          li: a(a href="#") Separated link
```

* navはHTML5要素
    * .navが基本クラス
    * .navbar-defaultは主に背景色(#f8f8f8)
        * 消去すると白地になる
        * .navbar-inverseで白黒反転(以前流行していたが見にくいので自分は嫌い)
* 内側のdiv.container-fluidで横幅一杯に取る(この中が実際のnavbarの内容)
* div.navbar-headerは全く説明がないので調べる
    * これはcollapse発生時にcollapseせずに残す部分
    * 内側にあるのは次の2つ
        * button.navbar-toggle(...)はcollapse時のみ表示する右端メニューボタン
            * data-toggle="collapse" でcollapse時のみ表示(JavaScript処理用)
            * data-target="{ID}"によりcollapse時にlink部を画面展開
                * {ID}は次のdiv.collapseのidに合わせる(変えると動かない)
            * span.icon-bar (x 3)はメニューボタン内の横線
                * 本数を変えると実際に確認できる
        * .navbar-brandはサイトのタイトル用(常に左端に大文字で表示)
* div.collapse.navbar-collapse#{id}もほぼ説明はない
    * .collapseは(たぶん)collapseする部分という意味
    * .navbar-collapseはその表示効果
    * IDが必要 - 手前のbutton-navbar(data-target='{ID}')で参照
    * collapse時にはこのdiv全体がdropdown itemsに変換される
* ul.nav.navbar-navはul.nav-tabsのnavbar版(これも説明なし)
    * 内部の書き方はほぼ同じ
    * b.caret (またはspan.caret)
        * exampleはb.caretを使っている
        * 両者を見比べても違いは分からない
* その内部はnavbarのメニューバー項目
    * li.dropdown
        * サブメニューなしの場合の内部
            * a(href='...') Description
        * サブメニュー(dropdown)ありの場合の内部
            * a.dropdown-toggle(href="#", data-toggle="dropdown")
               * | Item
               * b.caret
            * ul.dropdown-menu
                * li
                    * a(href="...") Item
* formはform.navbar-form
    * .navbar-formの効果は.form-inlineとだいたい同じ(横に並べる)
* 左右寄せは.navbar-left, .navbar-right (どちらも使われている)

これはさすがに大変だった(半日掛かったかも...)。それではまとめる。

まず外枠の構造は次の通り。これはほぼ決まり文句みたいなもの。

* nav.nav.navbar-default (反転時は.navbar-inverse)
    * div.container-fluid(横幅一杯) または .container (4段階に固定)
        * (Navbarコンテンツ)

上下スクロールしてもNavbarを上(下)端に固定して常に表示する場合。

* nav.nav.navbar-default.navbar-fixed-top (下端固定は.navbar-fixed-bottom)
    * div.container(-fluid)
        * (Navbarコンテンツ)

この場合はstylesheet側にも対応が必要。bootstrap.cssを読み込んだ後で次のような設定を追加する(上端固定の場合)。

``` jade
style(type='text/css').
  body { padding-top: 60px; }     // 本文は70だがこれくらいがちょうどいい
  // 下端の場合はpadding-bottom
```

> 他に.navbar-static-topという設定もあるが、本文を読んでも意味がよく分からないのでCSSを読んでみた。次のように設定する。
> 
> * padding-right: 0;
> * padding-left: 0;
> * z-index: 1000; (常に手前に表示)
> * border-width: 0 0 1px; (下線のみ表示)
> * モバイル(xs)ではさらに border-radius: 0; (角の丸めをなくす)
> 
> 実際に試してみてもデフォルト設定と大きな差はないが、内部要素の左右の配置が少しだけ変わる(おそらくpaddingの影響)。でもやっぱり何のために使うのか不明。

Navbarコンテンツをcollapse対応する場合の内部構造は次の通り。これもほぼ固定書式と考えてよい。

* div.navbar-header
    * button.navbar-toggle(type="button", data-toggle="collapse", data-target="#navbar-contents")
        * span.sr-only Toggle navigation (これはあった方が丁寧という程度)
        * span.icon-bar (x 横線の本数)
    * a.navbar-brand(href="#") ページ(サイト)のタイトル
* div.collapse.navbar-collapse#navbar-contents
    * Navbarコンテンツ

Navbarの内部では要素に専用クラスを用いる。

* form.navbar-form
* button.btn.navbar-btn
* p.navbar-text
* a.navbar-link

要素の左右寄せ(.pull-left/rightと同機能)も専用クラスを用いる。

* .navbar-left
* .navbar-right

## Breadcrumbs

現ページのサイト内の位置(階層)を表示するためのもの。

* ol.breadcrumb (ulでも同じ)

``` jade
ol.breadcrumb
  li: a(href="#") Home
  li: a(href="#") Library
  li.active Data
```

表示イメージ。

```
    Home  /  Library  /  Data
     ^         ^          ^
     |         |          |
 homeへの  Libraryへの  現在位置
  link       link       (linkなし)
```

## Pagination

ページアクセス用リンクのコントロール。

* ul.pagination
    * li.disabled - hoverしなくなる(でもクリックすると受け付ける)
    * li.active - 現在位置(同上)

``` jade
ul.pagination
  li.disabled: a(href='#') &laquo;
  li.active: a(href='#') 1
  li: a(href='#') 2
  li: a(href='#') 3
  li: a(href='#') 4
  li: a(href='#') 5
  li: a(href='#') &raquo;
```

サイズ指定(3段階)。

* .pagination-lg
* (なし)
* .pagination-sm

``` jade
- var sizes = [' pagination-lg', '', ' pagination-sm']
- for (var sz = 0; sz < sizes.length; ++sz)
  div
    ul(class = 'pagination' + sizes[sz])
      li: a(href='#') &laquo;
      - for (var i = 1; i <= 5; ++i)
        li: a(href='#')= "" + i
      li: a(href='#') &raquo;
```

## Pager

ページの前後移動用。

* ul.pager
    * li - デフォルトは中央に並べる
    * li.previous - 左寄せ
    * li.next - 右寄せ
    * li.disabled - grayed表示

``` jade
ul.pager
  // 左端に配置
  li.previous.disabled: a(href='#') &larr; first
  // 次の2つは中央に配置
  li.disabled: a(href='#') previous
  li: a(href='#') next
  // 右端に配置
  li.next: a(href='#') last
```

## Labels

反転して白抜き文字で表示する。背景色はオプションで選択する。

* span.label
    * .label-default
    * .label-primary
    * .label-success
    * .label-info
    * .label-warning
    * .label-danger

``` jade
- var opt = ['Default', 'Primary', 'Success', 'Info', 'Warning', 'Danger']
- for (var i = 0; i < opt.length; ++i)
  span(class = 'label label-' + opt[i].toLowerCase())= opt[i]
  = ' '
```

## Badges

「未読メッセージ数」のような場所に用いる。

* span.badge - 白抜きで背景の角を丸く表示

``` jade
p
  | inbox 
  span.badge 42
```

ボタンやnavbarの中など)反転している場所では再反転して白地で表示する。

``` jade
button.btn.btn-primary
  | Home 
  span.badge 42
```

## Jumbotron

全面表示。

* div.jumbotron
    * .containerの中ではcontainerの幅で角丸の背景
    * .containerの外では横幅いっぱい

``` jade
// container幅に角丸で表示
div.container
  div.jumbotron
    h1 Hello, world!
    p This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.
    p: a.btn.btn-primary.btn-lg(href='#') Learn more

// 横幅一杯に表示(divの入れ子を反転すればよい)
div.jumbotron
  div.container
    // 以下同じ(略)
```

## Page header

上マージンを多めに取る(h1に使う)。

> でも本文の意味がよく分からない(smallが何とかってどういう事?)。

* div.page-header

``` jade
// 普通のh1より上部の空白を広く取る
div.page-header
  h1 Example page header 
    small Subtext for header
```

## Thumbnails

全体をやや角を丸くした枠で囲む。

* .thumbnail

img.thumbnailはCSSの最後の方にすでに出てきている。実際に確認してみた

``` jade
// 134x180 empty image
- var imgUrl = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMzQiIGhlaWdodD0iMTgwIj48cmVjdCB3aWR0aD0iMTM0IiBoZWlnaHQ9IjE4MCIgZmlsbD0iI2VlZSI+PC9yZWN0Pjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIHg9IjY3IiB5PSI5MCIgc3R5bGU9ImZpbGw6I2FhYTtmb250LXdlaWdodDpib2xkO2ZvbnQtc2l6ZToxMnB4O2ZvbnQtZmFtaWx5OkFyaWFsLEhlbHZldGljYSxzYW5zLXNlcmlmO2RvbWluYW50LWJhc2VsaW5lOmNlbnRyYWwiPjEzNHgxODA8L3RleHQ+PC9zdmc+'
div.container
  div.row
    - for (var i = 0; i < 12; ++i)
      div.col-xs-6.col-md-3
        img.thumbnail(src = imgUrl)
```

img直接ではなく外側のdivに対して.thumbnailを適用できる。

``` jade
// 300x200 empty image
- var imgUrl = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIzMDAiIGhlaWdodD0iMjAwIj48cmVjdCB3aWR0aD0iMzAwIiBoZWlnaHQ9IjIwMCIgZmlsbD0iI2VlZSI+PC9yZWN0Pjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIHg9IjE1MCIgeT0iMTAwIiBzdHlsZT0iZmlsbDojYWFhO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1zaXplOjE5cHg7Zm9udC1mYW1pbHk6QXJpYWwsSGVsdmV0aWNhLHNhbnMtc2VyaWY7ZG9taW5hbnQtYmFzZWxpbmU6Y2VudHJhbCI+MzAweDIwMDwvdGV4dD48L3N2Zz4='
div.container
  div.row
    - for (var i = 0; i < 12; ++i)
      div.col-sm-6.col-md-4
        div.thumbnail
          img(src = imgUrl)
          h3 Thumbnail label
          p Cras justo odio, dapibus ac facilisis ...
          a.btn.btn-primary(href='#') Button
          |  
          a.btn.btn-default(href='#') Button
```

## Alerts

* div.alert
    * .alert-success (緑)
    * .alert-info (青)
    * .alert-warning (黄)
    * .alert-danger (赤)
    * .alert-dismissable (消去可能 - 例は後で示す)
    * a.alert-linkを内部で使うと
        * リンクの配色をalertの色とマッチさせる(若干濃い目で表示)

消去可能(dismissable)なalertの例(ついでにa.alert-linkも入れてみた)。

``` jade
div.alert.alert-danger
  button.close(type='button', data-dismiss='alert', aria-hidden) &times;
  strong Caution
  |  Please check 
  a.alert-link(href='#') your account.
```

難解なのはbuttonの部分だけ。ここは確認しておく。

* 表示効果は(.btnではなく).closeを使う
    * 右端にpull
    * 枠が付かない
    * 文字はopacityを設定して薄く表示
* aria-hiddenはaccessibility用属性(なくても動く)
* &times;(積算記号)は実は何でもいい
    * 「閉じる」等でもOKだが、普通の文字だと大きすぎて不釣り合い
    * これは.closeが表示効果を積算記号専用に調整しているため
* data-dismiss='alert'が機能上のポイント(bootstrap.jsがこれを検出して処理)

------------------------------------------------------------------------

(以下しばらく脱線)

機能上何が必須かはっきりしたので日本語サイト用に特化した例を作ってみた。

``` jade
// 日本専用サイト用
div.alert.alert-danger
  strong 注意: 
  | アカウント設定に問題があります。
  a.alert-link(href='#') 確認して下さい。
  button.btn.btn-danger.btn-xs.pull-right(type='button', data-dismiss='alert') 閉じる
```

* 「X」記号より「閉じる」の方が日本人には明解
* そこで(.closeは使わず)普通のbutton.btn.dangerを中に入れる
* .pull-rightで右に配置
* しかしボタンが高すぎてalertのboxと釣り合わないためサイズを調整
* .btn-xsで大体ちょうどよい(ぴったりではないが十分)

「閉じる」より「確認して...」の方がpriorityが高いので、できたらボタンをもっと目立たないようにしたい。

* ボタン色の変更は可能
    * 簡単に済ますなら例えば.btn-defaultに変更すればいい
    * 任意の表示効果にしたいならCSSを書いてoverrideすればどうにでもできる
* しかしそもそもこのケースではbuttonのpriortyが低い
    * そもそもdismiss(消去)処理は必須ではない(出したままで全操作可能)
    * 以下は'X"印と「閉じる」との比較検討
        * 'X'
            * 日本人にはちょっと分かりづらい点はある
            * でもuniversal designという点ではたぶんこれが一番だろう
        * 「閉じる」は日本語が分かる人専用
            * 分からない人には無意味な記号と同じ

以上総合すると...日本人専用サイトであれば有力という程度(いまいちだった...)。

------------------------------------------------------------------------

## Progress bars

> CSS3 transitionsを使っているので表示効果は機能しないブラウザが多い。

* div.progress - バーの下地、内側に次を挿入する
    * .progress-striped - 斜線付き
    * .progress-striped.active - 斜線 + アニメーション(IE9以下で動作しない)
* その内側に次を挿入
    * div-progress-bar(..., style='width:60%;')
        * style='width:xx%'で幅を設定
        * 内部に文字を書くとラベルになり中央に表示
        * 色設定は次の通り
            * (default) (blue)
            * .progress-bar-success (green)
            * .progress-bar-info (light blue)
            * .progress-bar-warning (orange)
            * .progress-bar-danger (red)
        * 複数使うと左側からstackする
        * aria-\*はaccessivility用(なくても描画はする)
    * その後にspan.sr-onlyで説明を付けるとfrendly

``` jade
div.progress
  div.progress-bar(aria-valuenow="60", aria-valuemin="0", aria-valuemax="100", style="width: 60%;")
    | 60%
span.sr-only 60% Complete
```

> aria-\*属性はWAI-ARIAに準拠したものと思われる。詳細は分からないがaccessibility対応であることは間違いない。
> 
> > (参考)WAI-ARIAの仕様書(でも今はとても読んでいる暇がない)。
> > 
> > <http://www.w3.org/WAI/PF/aria/>

以下は最低限機能させる場合の例(aria-\*属性は割愛)。

``` jade
// 基本
div.progress
  div.progress-bar(style="width: 60%;") 60%

// 斜線 + アニメーション
div.progress.progress-striped.active
  div.progress-bar(style="width: 40%;") 40%

// stack + 色分け
div.progress
  div.progress-bar.progress-bar-success(style="width: 30%;") 30%
  div.progress-bar.progress-bar-info(style="width: 25%;") 25%
  div.progress-bar.progress-bar-warning(style="width: 20%;") 20%
  div.progress-bar.progress-bar-danger(style="width: 15%;") 15%
div.progress
  div.progress-bar(style="width: 60%;") 60%
```

## Media object

まずexampleのパターンを把握する。

* div.media (外枠)
    * a.pull-left (リンク + 左float) (pull-rightも可能)
        * img.media-object (アイコン等)
    * div.media-body (文章ブロックの外枠)
        * h4.media-heading (タイトル)
        * 後は本文
        * .media-bodyの中にさらにdiv.media以下をnestできる

``` jade
// 64x64 empty image
- var mediaObjUrl = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI2NCIgaGVpZ2h0PSI2NCI+PHJlY3Qgd2lkdGg9IjY0IiBoZWlnaHQ9IjY0IiBmaWxsPSIjZWVlIj48L3JlY3Q+PHRleHQgdGV4dC1hbmNob3I9Im1pZGRsZSIgeD0iMzIiIHk9IjMyIiBzdHlsZT0iZmlsbDojYWFhO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1zaXplOjEycHg7Zm9udC1mYW1pbHk6QXJpYWwsSGVsdmV0aWNhLHNhbnMtc2VyaWY7ZG9taW5hbnQtYmFzZWxpbmU6Y2VudHJhbCI+NjR4NjQ8L3RleHQ+PC9zdmc+'

// 基本
div.media
  a.pull-left(href='#')
    img.media-object(src = mediaObjUrl)
  div.media-body
    h4.media-heading Media-heading
    | Cras sit amet nibh libero, in gravida nulla...

// 基本 + nest
div.media
  a.pull-left(href='#')
    img.media-object(src = mediaObjUrl)
  div.media-body
    h4.media-heading Media-heading
    | Cras sit amet nibh libero, in gravida nulla...
    // 以下nest
    div.media
      a.pull-left(href='#')
        img.media-object(src = mediaObjUrl)
      div.media-body
        h4.media-heading Media-heading
        | Cras sit amet nibh libero, in gravida nulla...
```

ulを使う場合のパターンは次の通り。

* ul.media-list
* li.media (div.mediaに対応 - 外枠)
    * 以下は同様(項目だけ書く)
    * a.pull-left
        * img.media-object
    * div.media-body
        * h4.media-heading
    * 後は本文
    * .media-bodyの中にさらにdiv.media以下をnestできる
    * 内部にul.media-listをnest可能

これもexampleと同じ構造を作ってみた。

``` jade
// 64x64 empty image
- var mediaObjUrl = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI2NCIgaGVpZ2h0PSI2NCI+PHJlY3Qgd2lkdGg9IjY0IiBoZWlnaHQ9IjY0IiBmaWxsPSIjZWVlIj48L3JlY3Q+PHRleHQgdGV4dC1hbmNob3I9Im1pZGRsZSIgeD0iMzIiIHk9IjMyIiBzdHlsZT0iZmlsbDojYWFhO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1zaXplOjEycHg7Zm9udC1mYW1pbHk6QXJpYWwsSGVsdmV0aWNhLHNhbnMtc2VyaWY7ZG9taW5hbnQtYmFzZWxpbmU6Y2VudHJhbCI+NjR4NjQ8L3RleHQ+PC9zdmc+'

ul.media-list
  li.media
    a.pull-left(href='#')
      img.media-object(src = mediaObjUrl)
    div.media-body
      h4.media-heading Media-heading
      | Cras sit amet nibh libero, in gravida nulla...
    // nest
    ul.media-list
      li.media
        a.pull-left(href='#')
          img.media-object(src = mediaObjUrl)
        div.media-body
          h4.media-heading Media-heading
          | Cras sit amet nibh libero, in gravida nulla...
        // nest
        ul.media-list
          li.media
            a.pull-left(href='#')
              img.media-object(src = mediaObjUrl)
            div.media-body
              h4.media-heading Media-heading
              | Cras sit amet nibh libero, in gravida nulla...
    ul.media-list
      li.media
        a.pull-left(href='#')
          img.media-object(src = mediaObjUrl)
        div.media-body
          h4.media-heading Media-heading
          | Cras sit amet nibh libero, in gravida nulla...
  li.media
    // pull-rightの例
    a.pull-right(href='#')
      img.media-object(src = mediaObjUrl)
    div.media-body
      h4.media-heading Media-heading
      | Cras sit amet nibh libero, in gravida nulla...
```

## List group

リストを利用して縦一列の表のように表示する。パターンは次の通り。

* ul.list-group
    * li.list-group-item
        * span.badge - 右端にラベルを表示(pullするので本文の前後どちらでもOK)
        * 配色を使える
            * (なし)はwhite
            * .list-group-item-success (green)
            * .list-group-item-info (blue)
            * .list-group-item-warning (orange)
            * .list-group-item-danger (red)

``` jade
// 初戦負けちゃった...
ul.list-group
  li.list-group-item.list-group-item-success Kawashima
    span.badge 1
  li.list-group-item.list-group-item-info Honda
    span.badge 4
  li.list-group-item.list-group-item-warning Kagawa
    span.badge 10
  li.list-group-item.list-group-item-danger Nagatomo
    span.badge 5
```

同じクラス設定の組み合わせをdivとaに対しても使える。aの内部にcustom textを挿入できる。

* ul.list-group
    * a.list-group-item
        * .active (primary配色で表示)
        * aの内部用クラスの例
            * h4.list-group-item-heading
            * p.list-group-item-text

``` jade
div.list-group
  a.list-group-item.active(href='#')
    h4.list-group-item-heading Kawashima
    p.list-group-item-text GK
  a.list-group-item(href='#')
    h4.list-group-item-heading Honda
    p.list-group-item-text FW
  a.list-group-item(href='#')
    h4.list-group-item-heading Kagawa
    p.list-group-item-text FW
  a.list-group-item(href='#')
    h4.list-group-item-heading Nagatomo
    p.list-group-item-text DF
```

## Panels

タイトルバー(またはフッタ)付き囲み記事のような表示効果。パターンは次の通り。

* div.panel.panel-default
    * .panelはshadow用
    * .panel-defaultで外枠を描画
    * 色を付ける場合は.panel-defaultの代わりに次を使う
        * .panel-primary
        * .panel-success
        * .panel-info
        * .panel-warning
        * .panel-danger
* その内側に次を挿入
    * div.panel-heading (タイトル部 - optional)
        * 内部にh2.panel-title等を挿入可能(文字サイズを調整できる)
    * div.panel-body (本文)
        * .panel-bodyはpadding確保用
    * table.table (テーブル)
    * ul.list-group
        * 内部はもちろんli.list-group-item
    * div.panel-footer (フッタ - optional)

``` jade
// 単純な例
div.panel.panel-default
  div.panel-body Basic panel example

// heading付き
div.panel.panel-default
  div.panel-heading Panel heading
  div.panel-body Panel content

// heading付き(やや文字を大きく)
div.panel.panel-default
  div.panel-heading
    h2.panel-title Panel heading
  div.panel-body Panel content

// footer付き
div.panel.panel-default
  div.panel-body Panel content
  div.panel-footer Panel footer

// 各種contextual colors
- var context = ['primary', 'success', 'info', 'warning', 'danger']
- for (var i = 0; i < context.length; ++i)
    div(class = 'panel panel-' + context[i])
      div.panel-heading Panel title
      div.panel-body Panel content

// tableの例(次がんばろう!)
div.panel.panel-default
  div.panel-heading 2014 FIFA World Cup Brazil
  div.panel-body 日本代表
  table.table
    tbody
      tr
        th 位置
        th 背番号
        th 選手名
      tr
        td 監督
        td -
        td アルベルト ザッケローニ
      tr
        td GK
        td 1
        td 川島 永嗣
      tr
        td DF
        td 2
        td 内田 篤人
      tr
        td MF
        td 17
        td 長谷部 誠
      tr
        td FW
        td 13
        td 大久保 嘉人

// listの例
div.panel.panel-default
  div.panel-heading グループC
  ul.list-group
    li.list-group-item コロンビア
    li.list-group-item コートジボワール
    li.list-group-item 日本
    li.list-group-item ギリシャ
```

## Wells

シンプルな外枠を付ける。

* div.well
    * .well-lg - 枠のマージンを大きく
    * .well-sm - 枠のマージンを小さく

``` jade
div.well 通常のwell
div.well.well-lg 枠が広いwell
div.well.well-sm 枠が狭いwell
```


JavaScript
========================================================================
<http://getbootstrap.com/javascript/>

タイトルだけ見るとjQueryのようなJavaScript APIの説明と勘違いしてしまいそうだが、実はcomponentsの補足説明が大部分。またCrouselを始めここにしか書いてない機能もある。

## Overview

> この部分はむしろ最後にすべき。最初に読んでもなかなか意味は取れない。

ファイル構成を確認する。

* 一括の場合
    * bootstrap.min.js は十分小さい(32k、gzipすると10k以下)
    * CDN利用可能なので、結局こちらを利用することになると思う
* 個別モジュールのソースはGitHub repoにある
    * これはソース解読時に便利
    * しかしこれを単独に読み込むのは賢い方法ではない(次がmuch better)
* オフィシャルサイトではBootstrapをcustomizeする機能を用意している
    * <http://getbootstrap.com/customize/>
* でも大部分のケースではbootstrap.min.css(js)を使う方が総合的な効率はいいはず

> さっきソースを見てちょっと驚いたが行末にセミコロンがない...

その他の注意。

* `data`属性は(bootstrapが内部で使っているため)使用禁止
    * ソースを読むと分かる
* jQueryのバージョン依存性はbower.jsonに書いてある
    * 現在は ">= 1.9.0"

Bootstrapの表示機能の一部(例えばdropdown)はJavaScriptを使っている。JavaScriptを全て無効化するには次のコードを加える。

``` javascript
// jQueryとBootstrapのロード後
$(document).off('.data-api')
```

これだけなら単にbootstrap.jsを読まないのと同じだが、モジュール別にon/offすることもできる。名前空間を逆順に指定する点に注意(module名が先)。

``` javascript
$(document).off('.alert.data-api');   // alertだけ無効化
```

以下はAPIの基本的なルール。

* jQueryプラグインとして機能する
    * モジュールごとに同名メソッドを呼び出す
    * 戻り値はjQueryの(collection)オブジェクト
* 引数は文字列またはオプションハッシュ

> 「個々のplugin objectにはConstructorがある」という意味の記述がある。これはソースを読めば実際に確認できるが、通常気にする必要はない(少なくとも自分でコールする事はない)。

------------------------------------------------------------------------

(以下参考 - 全部読み終えた後で追加)

それよりある程度ソースを読めるようになっておいた方がいい(結局ひと通り目は通した)。ソースは末尾のセミコロンがない書き方で最初は驚いたが、少し調べてみたら実はこれが「最新」らしい。まず次を参照。確かにセミコロンは使うなと書いてある。

<https://github.com/styleguide/javascript>

理由として参照しているのが次の記事。

<http://mislav.uniqpath.com/2010/05/semicolons/>

その日本語要約。これを読めばだいたい分かる。

<http://2012.8-p.info/japanese/3/9/semicolon>

RubyやPythonなどはとっくの昔に煩わしいセミコロンを省略してしまっており、JavaScriptもかなり前にセミコロンなしでもよい構文に変更されている。

ただし後付けのため仕様に若干おかしな点があるのもよく知られている。そのため古典的な教科書(特にCrockfordの"The Good Parts")は「セミコロンは絶対付けろ!」と言っている(特にCrockfordの言い方はかなり高圧的で反発も多い)。

これに対抗するのが「行末セミコロンを意図的に書かない派」で、セミコロンなしで問題を生じる箇所だけ次行の先頭に何か置けばいいという主張は確かにうなずける(これでいちいち書く手間が省けるのならお安いもの)。

> 最近は「セミコロン省略 + カンマ行頭」という人(npmの作者)もいるとの事。カンマ先頭は最近のnodeモジュールによくあるが(express等)、セミコロン省略は今回が始めてだったのでちょっと調べてみた。

> > ちなみに自分はもうCoffeeScriptしか使わなくなってしまったので、こういうことには無頓着だった。

プラグインのソースに話を戻す。書き方は美しく統一されておりとても読みやすい。button.jsを例に構造を説明する。

* 先頭の`+function ($) {`の`+`はたぶん行末セミコロン対策(だが詳細は不明)
* クラス定義
    * コンストラクタにはcapitalizeしたモジュール名を使う - buttonならButton
    * その先はインスタンスメソッド定義(Button.prototype.setState = ...等)
* プラグインの定義:`function Pluin(option) {`
    * $('#id').button(...)で呼び出すbuttonメソッドはこれ
* no conflict対策
* 最後にdata-\*属性に対する動作の実装(markup対応)
    * この部分がよくできているため通常はJavaScriptコードを書かなくていい

------------------------------------------------------------------------

Bootstrapプラグインはbuttonやalertというようなよくある名前なので他のプラグインと衝突する可能性が大きい。Bootstrapプラグインはロード時にプラグインプロパティ名の登録前の値を記憶しており、衝突した場合はnoConflictで元に戻せる。

``` javascript
// 先に何か別のbuttonプラグインをロードし、
// その後でBootstrapのbuttonプラグインをロードしたとする
var bootstrapButton = $.fn.button.noConflict()  // $.fnは$.prototypeと同じ
// これで先にロードしたbuttonプラグインが復活し、
// 戻り値としてBootstrapのbuttonプラグインが返る

// Buttostrapのbuttonプラグインを別の衝突しない名前で再登録
$.fn.bootstrapBtn = bootstrapButton
// 以下 $(...).bootstrapBtn(...) とコールすればよい
```

> 本文の説明を読むよりもソースを読んだ方が分かりやすい。前の値はoldという内部変数に束縛している。

イベント処理にはカスタムイベントを用い、jQueryの`on()`で登録する。各モジュール解説のEventsの節に例文がある(見れば使い方はおのずと分かる)。

> 最後のwarningにはちょっと注意。これを読むとconflict対策のためnoConflictを付けたりイベント名にnamespace化したが、それでもまだPrototypeやjQuery UIで対応しきれない状況が生じるらしい。

## Transitions

CSS transitionのサポート有無を判定し、サポートしていない場合はemulatorコードを用いるためのモジュール(他のモジュールがこれを利用する)。これは内部用なのでスキップする。

## Modals

まずモーダルダイアログの作り方から学ぶ(ただしこれだけだとstaticで表示するだけ)。

``` jade
// .modal.fadeを付けると表示してくれないので外す
div
  div.modal-dialog
    div.modal-content
      div.modal-header
        button.close(type="button", data-dismiss="modal") &times;
        h4.modal-title Modal title
      div.modal-body
        p One fine body&hellip;
      div.modal-footer
        button.btn.btn-default(type="button", data-dismiss="modal") Close
        button.btn.btn-primary(type="button") Save changes
```

* div.modal.fadeとすると表示しない(どちらもmodal動作用なので当然の結果)
* 以下のクラスは着脱して実際に表示効果を確認した
    * .modal-dialogは周囲とのマージン確保
    * .modal.contentは外枠とshadow
    * .modal-header/body/footerはその名の通り

それではこれをボタンでモーダル表示する。

* トリガするボタンの設定は次の2つ
    * data-toggle="modal"
    * data-target="#{ID}"
* div.modal.fade#{ID} が外枠
    * .modalが機能の設定(通常時は全体を非表示にするためこれが必須)
    * .fade は表示効果(なくてもいい: 消去すると一瞬で表示する)
    * IDは必須
    * aria-hidden="true"は機能的には必須(JavaScriptで使う)だが省略可能
        * 省略するとJavaScriptが自動的に付ける
        * 非表示時はtrue, 表示時はfalseに設定
    * その他の属性ははなくても動く
        * tabindexは意味不明(-1なので「最優先で受ける」という意味だが...)
        * role="dialog"はaccessibility用にあった方が丁寧
        * aria-labelled-by="{ID}"の参照先は内部のh4要素
            * これもあれば丁寧という程度、消去しても動く
* その内側はdiv.modal-dialog
    * .modal-dialogが基本の表示効果(外枠とshadow)
    * サイズ設定は3種類(次のクラスを追加して設定)
        * .modal-lg - 幅をいっぱいに広げる
        * (デフォルト)
        * .modal-sm - 幅を狭く

最低限動作する設定で作ってみた。

``` jade
button.btn.btn-primary.btn-lg(data-toggle="modal", data-target="#myModal")
  | Launch demo modal

div.modal.fade#myModal(aria-hidden="true")
  div.modal-dialog
    div.modal-content
      div.modal-header
        button.close(type="button", data-dismiss="modal") &times;
        h4.modal-title Modal title
      div.modal-body Modal body
      div.modal-footer
        button.btn.btn-default(type="button", data-dismiss="modal") Close
        button.btn.btn-primary(type="button") Save changes
```

横幅設定の例。

``` jade
- var sizes = ['lg', 'md', 'sm']
- for (var i = 0; i < sizes.length; ++i)
  button.btn.btn-primary(data-toggle="modal", data-target="#myModal-" + sizes[i])
    = 'Launch ' + sizes[i]
  = ' '

- for (var i = 0; i < sizes.length; ++i)
  div.modal.fade(id = 'myModal-' + sizes[i])
    // .modal-mdは意味なし(デフォルトサイズにしたいだけなのでOK)
    div(class = 'modal-dialog modal-' + sizes[i])
      div.modal-content
        div.modal-header
          button.close(type="button", data-dismiss="modal") &times;
          h4.modal-title Modal title
        div.modal-body Modal body
        div.modal-footer
          button.btn.btn-default(type="button", data-dismiss="modal") Close
          button.btn.btn-primary(type="button") Save changes
```

モーダル表示中はbodyに.modal-openを設定する。またbodyの子の末尾にdiv.modal-backdropを追加する(モーダルの外側の処理用: 背景を暗くする処理とクリックした時にモーダルを閉じるため)。

JavaScriptを使わずに処理する場合はもう自分で解析したがまとめておく。

* button側に次の属性を追加
    * data-toggle="modal"
    * data-target="#{ID}"
* div.modal(.fade)にIDを追加

JavaScriptを使う場合の例。argは文字列またはoption hash(詳しくは本文参照)。

``` javascript
// デフォルト
$('#myModal').modal();

// 強制的にclose
$('#myModal').modal('hide');

// backdropなし(背景が暗くならず、周囲をクリックしてもcloseしない)
$('#myModal').modal({backdrop: false});
```

Optionsはmarkup側からも利用できる。ここに書いてあるプロパティ名の先頭にdata-を付けた属性を要素に指定すれば機能する(以下全てのモジュールで同様)。

``` jade
// backdrop背景なし(data-backdrop=''でもよい)
button.btn.btn-primary.btn-lg(data-toggle="modal", data-target="#myModal" data-backdrop='false')
      | Launch demo modal
```

イベント処理の例。

``` javascript
$('#myModal-md').on('hide.bs.modal', function (e) {
  // close(CSS transision)開始
  console.log('modal is closing');
}).on('hidden.bs.modal', function (e) {
  // close終了(0.3s後)
  console.log('modal closed');
})
```

> transition時間はCSSの側で設定している。ここでの該当部分は.modal.fade。後はCSSソースを見れば分かる。
> 
> ちょっと時間がかかったが感覚はつかめた。以下加速して一気に終わらせる。

## Dropdowns

Exampleと同じnavbarを作ってみた(やっぱりけっこう大変: 30分以上はかかったか?)。

```
nav.navbar.navbar-default
  div.container-fluid
    div.navbar-header
      button.navbar-toggle(type='button', data-toggle='collapse', data-target='#navbar-collapse-1')
        span.sr-only Toggle navigation
        - for (var i = 0; i < 3; ++i)
          span.icon-bar
      a.navbar-brand(href="#") Project name

    div.collaps.navbar-collapse#navbar-collapse-1
      ul.nav.navbar-nav
        - var dropdowns = ['Dropdown', 'Dropdown 2']
        - for (var i = 0; i < dropdowns.length; ++i)
          li.dropdown
            a.dropdown-toggle(href="#", data-toggle="dropdown")
              = dropdowns[i] + ' '
              b.caret
            ul.dropdown-menu
              li: a(href="#") Action
              li: a(href="#") Another action
              li: a(href="#") Something else here
              li.divider
              li: a(href="#") Separated link
              li.divider
              li: a(href="#") One more separated link

      // .navbar-rightはこのレベルでないと機能しない(ここで苦労した)
      // (もう一段内側のli.dropdownに付けられれば上のループと一緒にできるのに)
      ul.nav.navbar-nav.navbar-right
        li.dropdown
          a.dropdown-toggle(href="#", data-toggle="dropdown") Dropdown 3 
            b.caret
          ul.dropdown-menu
            li: a(href="#") Action
            li: a(href="#") Another action
            li: a(href="#") Something else here
            li.divider
            li: a(href="#") Separated link
            li.divider
            li: a(href="#") One more separated link
```

Pillsなら簡単。こちらは10分でできた。

```
ul.nav.nav-pills
  li.active: a(href='#') Regular link
  - var dropdowns = ['Dropdown', 'Dropdown 2', 'Dropdown 3']
  - for (var i = 0; i < dropdowns.length; ++i)
    li.dropdown(id = 'dropdown-' + i)
      a.dropdown-toggle(href='#', data-toggle='dropdown')
        = dropdowns[i] + ' '
        span.caret
      ul.dropdown-menu
        li: a(href="#") Action
        li: a(href="#") Another action
        li: a(href="#") Something else here
        li.divider
        li: a(href="#") Separated link
```

クリックすると起点となる要素(上記の場合はli.dropdown)に.openを追加してul.dropdown-menuを表示する、また外側には外部クリックでdropdownを閉じるための.dropdown-backdropを追加する。

> FirebugやChrome devtoolを使い、.dropdownに.openが追加されるのは確認できた。しかし.dropdown-backdropはどうしても見つけることができない(今はもう方法が変わっているのかも知れない)。

基本パターンをまとめてみる。

```
(通常は)div.dropdown (囲み用要素)
  (aまたはbutton)(data-toggle='dropdown')
  ul.dropdown-menu
    li
      a(href='...') ...
    li ...
      a(href='...') ...
    ...
```

* 囲み用要素にはいくつかバリエーションがある(おかげでまとめるのに苦労した)
    * div.dropdown(内部の要素にaやbuttonを用いる場合、これが一番多い)
    * (参考)span.dropdownも試してみたがちゃんと機能した
    * li.dropdown(navやnavbarのitemの場合)
    * div-btn-group(ボタングループの中にdropdownを入れる場合)
* 次はdropdownクリックを受け付ける要素
    * (aまたはbutton)(data-toggle='dropdown')
        * data-toggle='dropdown'が必須の属性(ないとpluginが認識しない)
    * その他のオプション
        * .dropdown-toggleは表示効果用だが、なくても機能はする
            * Componentsのexampleはほぼ付けているが、本sectionには付いてない
        * href='#'はaの場合に必要(hoverした時にcursor形状を変える効果)

> data-targetに関する説明が意味不明。a(... data-target='#', href='/page.html')としてみた所で、これはメニューバーの部分なのでクリックするとropdownするだけで/page.htmlにはリンクしない。

なおButtonの中にdropdownを入れる場合の外枠はdiv.dropdownとdiv.btn-groupのどちらでもよい。ただし.btn-groupが必須なのはボタングループ内のボタンにdropdownを挿入する場合(nesting)だけなので、それ以外はdiv.dropdownを使う方が明解だと思う。

JavaScriptインターフェースはもう特筆すべきことはないので(たぶんその先ずっと)略(十分感じは分かった)。

ここでjadeの:coffeeフィルタを使いCoffeeScriptで記述する方法を試してみた(やはりこの方が楽)。jade経由だとこういうところも便利。

``` jade
  script
    :coffee
      $('#dropdown-1').on 'show.bs.dropdown', -> console.log 'show'
      $('#dropdown-1').on 'hide.bs.dropdown', -> console.log 'hide'
```

## Scrollspy

ここは詳しい説明は略。ただし一回実際に作ってみる。

``` jade
// やや不完全(動くが要オフセット調整:本来bodyを想定したものなので仕方ない)
div.container
  // navにIDを設定するのがまず第一のポイント
  nav.nav.navbar-default.navbar-static#navbar-chapters
    div
      ul.nav.navbar-nav
        - for (var chap = 1; chap <= 5; ++chap)
            li.dropdown
              a.dropdown-toggle(data-toggle='dropdown', href='#' + chap)
                = "Chapter " + chap + ' '
                b.caret
              ul.dropdown-menu
                - for (var sect = 1; sect <= 5; ++sect)
                  li
                    a(href='#' + chap + '-' + sect)
                      = "Section " + chap + '-' + sect

// こちらが「監視対象」: 本来は(本文通り)bodyに設定すべきところ
// 必須属性はdata-spy="scroll"とdata-target="navのID"の2つ
// また(bodyでなく)中途半端な場所から始まるためdata-offsetを調整している
// (data-offset="上端からのpixel距離" - 適宜調整すること)
div.container(data-spy="scroll", data-target='#navbar-chapters', data-offset="120", style='height: 200px; overflow: auto;')
  - for (var chap = 1; chap <= 5; ++chap)
    h2(id = '' + chap)= "Chapter " + chap
    - for (var sect = 1; sect <= 5; ++sect)
      h3(id = '' + chap + '-' + sect)= 'Section ' + chap + '-' + sect
```

## Togglable tabs

Navsで学んだ通り.nav.tabs/pillsのデフォルト動作はstaticだが、少しだけ手を加えればdynamicな動作を実現できる。これもexampleとほぼ同じレイアウトのものを作ってみた(周囲にpanelを使う例)。

``` jade
div.panel.panel-default
  div.panel-body
    ul.nav.nav-tabs
      li.active
        a(href='#home', data-toggle='tab') Home
      li
        a(href='#profile', data-toggle='tab') Profile
      li
        a(href='#contact', data-toggle='tab') Contact

    div.tab-content
      div.tab-pane.active#home
        div.panel-body Home
      div.tab-pane#profile
        div.panel-body Profile
      div.tab-pane#contact
        div.panel-body Contact
```

* ul.nav.nav-tabs(または.nav-pills)
    * liの内部のa(href="ID")全てにdata-toggle='tab'を追加(必須)
    * liの一つに.activeを追加(これが初期状態で表示される)
* div.tab-content
    * div.tab-pane#ID がタブの中身
    * 最初に表示するものをdiv.tab-pane.activeとする

> 機能実装は難しくないが、それよりマージン調整の方がややこしい。特に.panel-bodyをどの階層に用いるかで余白がころころ変化する。ただしここの本題とは関係ないので深入りしない。

fade効果を加える場合は次の通り変更すればよい。

``` jade
    div.tab-content
      div.tab-pane.active.fade.in#home
        div.panel-body Home
      div.tab-pane.fade#profile
        div.panel-body Profile
      div.tab-pane.fade#contact
        div.panel-body Contact
```

* active項目は.fade.inを追加(.inを忘れると最初の時表示してくれない)
* その他は.fadeを追加

## Tooltips

Tooltipはname属性をサポートする任意の要素(典型的にはaとbutton)に付けられる。name="説明"を書けばhoverした時に小さなpopupが表示される。これはHTML5対応のmodern browserならすべてサポートしている。

``` jade
a(href='#', title='TOOLTIP!') tooltip
```

BootstrapはJavaScriptを用いた拡張機能がある。ただしデフォルトではこの機能は無効になっており、起動する場合は簡単なJavaScriptコードを追加する必要がある。

``` jade
  script
    $('a').tooltip();     // 例: 全てのa要素に対して有効化
```

これでhoverした時にpopupするtooltipの形状が漫画の吹き出しのような形状になり、以下説明する各種optionも使えるようになる。

> exampleには全てdata-toggle='tooltip'も設定されているが実際には不要。しかしブラウザに依存している可能性は考えられる。ここでは付けないが、本番で使うときは付けておいた方が無難だと思う。

Optionの例。

``` jade
// 右側に表示、500msのdelayを追加
a(href='#', title='TOOLTIP!', data-placement='right', data-delay='500') tooltip

// htmlを有効にして赤の強調文字で表示
    a(href='#', title="<span style='color:red;'><b>TOOLTIP!</b></span>", data-html='true') tooltip
```

## Popovers

Popoverはtooltipよりも大きいpopup paneで、title(タイトルバー)と(data-)content(本文)を表示できる。また(hoverではなく)clickで表示/非表示をtoggleする(optionで変更可能)。

これもtooltipと同様に初期状態は無効化されているので、次のように起動する。

``` javascript
$('#example').popover(/*options*/)
```

最低限の例。

```
button.btn.btn-default#example(type='button', title='Popover', data-content='This is a popover message.') Click me
```

* title='Popover'はタイトルバー
* data-contentが本文
* data-toggle='popover'は不要(でもないと動作しないブラウザがあるかも...)

その他の細かい点はOptionsを参照。例えばclickではなくhoverに対して表示させる場合はdata-trigger='hover'とすればよい。

## Alert messages

ここはalertをcloseするためのJavaScript機能の説明。もう自力で調べ終わっているがもう一度確認する。まずは典型的な文例。

``` jade
div.alert.alert-info.fade.in
  button.close(type='button', data-dismiss='alert') &times;
  strong Info:
  |  Dismissable alert example.
```

Dismissable alertをmarkupだけで動作させるのに最低限必要な条件は次の通り(これも調査済み)。

* 外枠は任意のbloock/inline要素でいい(ただのspanでも動いた)
    * 内側にbutton(data-dismiss='alert')
        * type='button'やaria-\*などはなくても動く(もちろんあった方が丁寧)

その他の設定は全てCSSの表示効果。テンプレートは次の通り。

``` jade
div.alert.alert-{種類}[.fade.in]
  button.close(type='button', data-dismiss='alert') &times;
  strong {ヘッダ}
  |  {本文}
```

* .alertは領域とマージンの確保用
* .alert-{種類}(default/success/info/warning/danger)は表示効果(特に背景色)
* dismiss時にフェードアウト効果を付ける場合は.fade.inを追加
    * .fadeがtransition効果
    * .inは「初期化時に表示」(忘れるとロード時に表示しない)
* .closeは表示効果(右にpull、若干大きめ(?)の太字、透過率を設定して薄く表示)
* &times;は'X'印(.closeの設定はこの文字の表示に特化したもの)
* 以下コンテンツ
    * 先頭にタイトル(strong要素)付きのタイトル
    * 間に空白文字(入れないとくっつく)
    * その後に本文

## Buttons

ここはcomponentsでまだ説明してなかったbuttonの機能(続き)。

Load実行中に表示が変わるボタンの例。まずはHTML側に次を追加する。

* data-loading="ロード中に表示する文字列" を追加

``` jade
button.btn.btn-primary#btn-load(type='button', data-loading-text='Loading...') Load
```

これは自動的には切り替わってくれない(要JavaScript)。次のようなコードを加える。

``` coffeescript
# 場所に注意: jQueryとbootstrap.jsの後でないと動作しない
# (おっとここだけCoffeeScriptで書いてしまった)
$('#btn-load').click ->
  btn = $ @
  btn.button 'loading'
  # 本当は$.ajaxだがテスト用にtimerを使う(2s後に復帰)
  setTimeout((-> btn.button 'reset'), 2000)
```

ここで$(...).button(...)はBootstrapのbuttonモジュール(jQueryプラグイン)。後ろのMethodsの節に説明がある。上記コードで行っていることは次の通り。

* $(...).button('loading') でロード中の状態に設定
* $(...).button('reset') で元に戻す

> 本文の説明は十分ではない(特に'reset'の記述なし)。ここはコード(button.js)を読むこと。プラグイン関数定義はfunction Plugin ...の部分。状態設定はsetState(ここを読めば'reset'を認識することが分かる)。

後はmarkupだけでできる処理(コード不要)。

* 単独トグルの場合はbuttonにdata-toggle="button"を追加
* グループの場合はdiv.btn-groupにdata-toggle="buttons"(複数形)を追加
    * label.btn.btn-{TYPE} がボタンの表示効果
        * 内部はinput(type='checkbox'または'radio')

``` jade
// 全体的にボタン色が分かりにくいのでbtn-defaultに変更

// 単独トグル(ただし動作に問題あり、後で補足する)
button.btn.btn-default(type='button', data-toggle='button') Toggle

// チェックボックスグループ
div.btn-group(data-toggle='buttons')
  - for (var i = 1; i <= 3; ++i)
    label.btn.btn-default
      input(type='checkbox')
      = 'Option ' + i

// ラジオ動作
div.btn-group(data-toggle='buttons')
  - for (var i = 1; i <= 3; ++i)
    label.btn.btn-default
      input(type='radio', name='radio-example')
      = 'Option ' + i
```

なお状態の表示効果にやや分かりにくい点がある(もし自分が担当者なら改良する)。

* check状態は背景を濃くする(これはいいとして...)
* clickやfocus/hoverなどの状態でも背景を濃くする(色は同じ)
* 違いはcheck状態の場合に(linear-gradientの)shadowがかかることだけ

この違いはbtn-defaultのような明るい背景色ならよく分かるが、btn-primaryのような濃い背景色だとほとんど区別が付かない。確認用に次を作ってみた。

``` jade
// 背景色の比較用
- var colors = ['default', 'primary', 'success', 'info', 'warning', 'danger', 'link']
// checkboxの場合
- for (var c = 0; c < colors.length; ++c)
  div.btn-group(data-toggle='buttons')
    - for (var i = 1; i <= 3; ++i)
      label(class = 'btn btn-' + colors[c])
        input(type='checkbox')
        = '' + i
br
// radioの場合
- for (var c = 0; c < colors.length; ++c)
  div.btn-group(data-toggle='buttons')
    - for (var i = 1; i <= 3; ++i)
      label(class = 'btn btn-' + colors[c])
        input(type='radio', name='radio-example-' + colors[c])
        = '' + i
```

やはりdefaultならよく分かるが、それ以外はやはり少し見にくい(判別が難しい)。またradioは1つcheckすると他が外れるのでまだ判別しやすいが、checkboxは個々のボタン変化しかないので判別がより困難になる。

また単独toggle check buttonには別の問題があり、checkを解除してマウスボタンを離しても色が変化せず、別の場所をクリックしてようやく色が元に戻る(これはさすがに不具合と考えるべきだが、現在の仕様ではこの動作にしかできないのかも知れない)。

これはボタンが1つだけのcheckboxグループにすれば解決できる。

``` jade
// 単独トグルの改善策
div.btn-group(data-toggle='buttons')
  label.btn.btn-default
    input(type='checkbox')
    | Toggle
```

## Collapse

Exampleを見る限りこれはjQuery UIなど他のライブラリのaccordionと同じ機能。表示にはpanelを使い、動的な効果を加える。これは自分で作ってみた方が早い。

``` jade
div.panel-group#accordion
  - for (var i = 1; i <= 3; ++i)
    div.panel.panel-default
      div.panel-heading
        h4.panel-title
          a(data-toggle="collapse", data-parent="#accordion", href="#collapse-" + i)
            = 'Collapsible Group Item #' + i
      - var klass = 'panel-collapse collapse'
      - if (i == 1) klass += ' in'
      div(class = klass, id = 'collapse-' + i)
        div.panel-body
          = 'Collapsible Group Item contents #' + i
```

明確なパターンがある。パネルの色以外にオプションらしいものはない。

* 外側はdiv.panel-group#{親ID} (このIDは必須)
    * div.panel.panel-{context} (contextはdefaultなどの色設定)
        * div.panel-heading
            * h4.panel-title
                * a(data-toggle="collapse", data-parent="#{親ID}", href="#{コンテンツボディID}") タイトル文字列
        * div.panel-collapse.collapse#コンテンツボディID[.in]
            * div.panel-body
                * ボディ文書

機能上必要な項目は次の通り。

* 親divのID
* aの次の属性(全部必要)
    * data-toggle="collapse"
    * data-parent="#{親ID}"
    * href="#{コンテンツボディID}"
* body部分のdivの設定
    * #コンテンツボディID
    * .collapse (これで初期状態は表示しない)
    * 初期状態で表示するものだけ.collapse.in
    * (参考) transition中は.collapsingに変化する(自動的に設定される)

一つの場合はもっと簡単にできる。

``` jade
div.panel.panel-info
  div.panel-heading
    h4.panel-title
      a(href='#', data-toggle="collapse", data-target="#collapse-1")
        | Collapsible Item #1
  div.panel-collapse.collapse.in#collapse-1
    div.panel-body Collapsible Item contents #1
```

この場合は必要なものが少し異なる。

* クリック受信要素(上記の場合はa)の次の属性
    * data-toggle="collapse"
    * data-target="コンテンツID"
* コンテンツ要素の次の属性
    * .collapse[.in]
    * #コンテンツID

なおhref='#'の意味はカーソル形状をポインタにするためだが、これだとURLが'#'に遷移する。これがいやならspanなどの要素に変更してstyleでマウスカーソルを設定すればよい。

``` jade
      // a(href='#', data-toggle="collapse", data-target="#collapse-1")を変更
      span(data-toggle="collapse", data-target="#collapse-1", style='cursor:pointer;')
```

なお条件さえ満たしていればpanelと無関係な要素でも機能する。buttonとwellで作った場合は次の通り(wellの方が構造が簡単なので2要素だけで作れる)。

```
button.btn.btn-danger(type="button", data-toggle="collapse", data-target="#demo") simple collapsible
div.well.collapse.in#demo Collapsive well.
```

> しかしwellだとtransitionが何だかぎこちなくなる。CSSの書式や表示効果はpanelに合わせて作ってあるのでこれは仕方ないだろう。

## Carousel

最近いろいろなサイトでよく見るスライド表示。まずは作ってみる。

``` jade
// 画像データ
- var slide1 = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI5MDAiIGhlaWdodD0iNTAwIj48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjUwMCIgZmlsbD0iIzc3NyI+PC9yZWN0Pjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIHg9IjQ1MCIgeT0iMjUwIiBzdHlsZT0iZmlsbDojNTU1O2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1zaXplOjU2cHg7Zm9udC1mYW1pbHk6QXJpYWwsSGVsdmV0aWNhLHNhbnMtc2VyaWY7ZG9taW5hbnQtYmFzZWxpbmU6Y2VudHJhbCI+Rmlyc3Qgc2xpZGU8L3RleHQ+PC9zdmc+'
- var slide2 = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI5MDAiIGhlaWdodD0iNTAwIj48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjUwMCIgZmlsbD0iIzY2NiI+PC9yZWN0Pjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIHg9IjQ1MCIgeT0iMjUwIiBzdHlsZT0iZmlsbDojNDQ0O2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1zaXplOjU2cHg7Zm9udC1mYW1pbHk6QXJpYWwsSGVsdmV0aWNhLHNhbnMtc2VyaWY7ZG9taW5hbnQtYmFzZWxpbmU6Y2VudHJhbCI+U2Vjb25kIHNsaWRlPC90ZXh0Pjwvc3ZnPg=='
- var slide3 = 'data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI5MDAiIGhlaWdodD0iNTAwIj48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjUwMCIgZmlsbD0iIzU1NSI+PC9yZWN0Pjx0ZXh0IHRleHQtYW5jaG9yPSJtaWRkbGUiIHg9IjQ1MCIgeT0iMjUwIiBzdHlsZT0iZmlsbDojMzMzO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1zaXplOjU2cHg7Zm9udC1mYW1pbHk6QXJpYWwsSGVsdmV0aWNhLHNhbnMtc2VyaWY7ZG9taW5hbnQtYmFzZWxpbmU6Y2VudHJhbCI+VGhpcmQgc2xpZGU8L3RleHQ+PC9zdmc+'
- var slides = [slide1, slide2, slide3]

// ここにIDが必要(複数のcarouselsが同時に動作する場合を考えて...)
div.carousel.slide#carousel-example-generic(data-ride="carousel")
  // indicator(中央下部の丸)
  ol.carousel-indicators
    - for (var i = 0; i < 3; ++i)
      li(data-target="#carousel-example-generic", data-slide-to="" + i, class= (i == 0) ? "active" : "")
  // スライドイメージとキャプション
  div.carousel-inner
    - for (var i = 0; i < 3; ++i)
      div(class = 'item' + ((i == 0) ? ' active' : ''))
        // 画像
        img(src=slides[i])
        // キャプション(タイトルと説明)
        div.carousel-caption
          h4= "Slide " + (i + 1)
          p= "Slide number-" + (i + 1)
  // 左矢印
  a.left.carousel-control(href="#carousel-example-generic", data-slide="prev")
    span.glyphicon.glyphicon-chevron-left
  // 右矢印
  a.right.carousel-control(href="#carousel-example-generic", data-slide="next")
    span.glyphicon.glyphicon-chevron-right
```

(ちょっと大変だったが、逆に言えば...)たったこれだけでできる。さすがに疲れてきたので動作確認だけして終わりにする。

> 完璧に動作した。後で何か作るときはこれをコピペすればよい。

## Affix

Affixとはこのマニュアルドキュメントの右端に表示されるナビゲーションのこと。これはさすがに省略する(説明も少ないので詳細は自分で調べるしかない)。

> 動作に不安定な部分がある。特に画面幅の変更に対して対応できておらず、幅を一旦狭くして(消去される)、縦スクロール後にもう一度拡げても復活しない(Affixが行方不明になる)。


Customize and download
========================================================================
<http://getbootstrap.com/customize/>

このWebページを使ってBootstrapを自分の好きなようにカスタマイズできる。

> いまのところその気はないが、何ができるかはちゃんと調べておく。

## Less files

Lessソースのどの部分だけ使うかを選択できる。使わないものを消去する場合はありだと思うが(例えばTable/Pagination/Jumbotron/Carouselは使わない等)、使うものだけpickしても依存性があるのでまともには動かないような気がする。

## jQuery plugins

これも同上。ただし数が少ないので依存性で悩むことはあまりないだろう(最悪でも試行錯誤数回程度で解決できるはず)。

> ただしこうやってサイズ削減するよりCDNを使った方がおそらくパフォーマンスは上だし、だいいちめんどくさくない。

## Less variables

ここがある意味白眉(?)。表示の設定(色、フォント、余白等)は全てここで変更できる。しかし項目数があまりに多すぎて現実味がなくなっている感じもする。

ただしここを眺めているだけでBootstrapの作りをある程度把握できるし、Lessソースを見るときの参考用としてとてもよい(変数名と意味が一目瞭然)。それだけでも十分価値はあると思う。

## Download

全部設定したらここからdownload実行!...しかしこんな大変な作業を本気でやる人が果たしているのだろうか?

やはりformでこんな膨大なデータを送るのは現実的ではないし、ちょっと失敗したからやり直し...という状況が一番困る(もう一回全部打ち込めっていうのか?)。

それよりGitHub repoのソースを自分で変更して作業した方がずっと効率はよいし、何度でもやり直しが効く。ファイル生成方法はGruntfileを見ればいい(grunt.registerTask(...)の部分がtarget設定)。

> このページは開発者が「こういうこともできます」というデモみたいなものだと思った方がいいかも知れない。またここを見ればBootstrap全体の構成を把握できるので、そういう意味でたとえカスタマイズする気がなくても一度目を通すといい。
