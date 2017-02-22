# 画随音动！Web Audio API入门（四）

***

>* 原文链接 : [音にあわせて画面が変化！続々々「WebAudioAPI」入門](https://liginc.co.jp/310761)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

今回は、音源の解析と、その結果の視覚化について紹介します。

> ・この記事を読むときは、お使いのブラウザの他のタブ、ウインドウでWebAudioAPIが使用されていないことをご確認願います。
・コードプレビューのJS全体が即時関数で囲われている場合、その即時関数は実際には不要であると考えてください。
> Webブラウザは同時に存在できるAudioContextオブジェクトの数に制限をかけています。
通常、AudioContextオブジェクトが1アプリケーションに複数必要となることはなく、この制限に困ることはありません。
ただし、複数のタブ、ウインドウ、iframeでWebAudioAPIが使用される場合にはエラー発生の可能性があるため、本記事では処理を即時終了させることで対策を行っております。

## 音源の情報を解析し視覚化するWebサイト
### Loop Waveform Visualizer

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/06/waa03.png)

[https://airtightinteractive.com/demos/js/reactive](https://airtightinteractive.com/demos/js/reactive)
こちらは、以前にも紹介した音源を再生しながら視覚化するWebサイトです。

mp3ファイルを画面にドロップ、もしくは「load sample mp3」をクリックすると再生が始まります。

このサイトでは、瞬間瞬間の音量をWebAudioAPIによって解析し、音量の値が反映された円形をThree.jsによって描画することで、視覚化を実現しています。
音声ファイルの扱いに関してはこれまでの記事でも紹介してきましたので、この記事では、解析対象をマイクからの音声に置き換えてみましょう。

## 「Web Audio API」を使って音にあわせて画面を変化させてみよう

### マイクから取得した音を音源として利用してみる

音声や動画などのメディアコンテンツは、MediaStreamオブジェクトとして表現されます。MediaStreamオブジェクトは、navigator.mediaDevicesオブジェクトのメソッド、getUserMediaによって取得します。

このMediaStreamオブジェクトをWebAudioAPIから扱うには、MediaStreamAudioSourceNodeというAudioNodeを使用します。

>【getUserMediaを使用する上での注意】

getUserMediaを使用する場合は、下記の3点に注意する必要があります。

1. Safari(Mac/iOSとも)未対応

  現状ではMac,iOS両方のSafariにまだ実装されていません。
  というわけで、今回の内容はスマートフォン対象外となります……つらい。
2. ポリフィルが必要

  getUserMediaは、以前navigatorオブジェクトのメソッド（navigator.getUserMedia）として実装されていましたが、現在そちらの実装は非推奨となっています。そのため、すべてのブラウザでnavigator.mediaDevices.getUserMediaとしてこのメソッドを利用するには、ポリフィルを用意する必要があります。詳しくはMDNをご参照ください。
  以降に埋め込んでいるコードプレビューでも、MDNで紹介されているものを参考としたポリフィルを用意し、あらかじめ読み込んでいます。
3. HTTPSでアクセスしたページでないと使用できない

  getUserMediaは、セキュリティ対策のため、HTTPS（暗号化通信）でアクセスしたページでなければ失敗するように実装されています。現在では、GithubPagesやCodePen、Netlifyなど、無料サービスでも暗号化通信が有効である場合が多いです。
  個人で証明書を発行することが難しい場合は、ぜひこれらを活用してみてください。

ではまず、最終出力に直接つないでみましょう。
以下のコードを、RESULTボタンで実行してみてください。

<p data-height="265" data-theme-id="0" data-slug-hash="jrbJGX" data-default-tab="js" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160901" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/jrbJGX/">160901</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

周囲の音がほんの少し遅れて聞こえてくる、そんな状態になっているかと思います。

MediaStreamオブジェクトは、生成された直後にマイクからの音声取得を開始し、その情報はリアルタイムに更新されていきます。MediaStreamAudioSourceNodeもまた、生成されたあと、他のAudioNodeに接続するとすぐ、出力を開始します。

マイクから音声を取得できることを確認できたので、次は音源を解析し、音量を取得してみましょう。

### 音源を解析して音量を取得してみる

解析処理は、AnalyserNodeというAudioNodeによって表されます。
AnalyserNodeは、音源を解析するメソッドをいくつか持っています。これらのメソッドは、それぞれ実行結果として得られる値の型が決まっており、それに対応する型付き配列をその格納先として必要とします。

今回はその中から、周波数ごとの波形の振幅を符号無しの8ビット整数、つまり0～255の範囲で表し、配列に格納するメソッド、getByteFrequencyDataを使用します。

実行結果として得られる値の型が符号無しの8ビット整数であるため、格納先として必要になる配列はUint8Arrayです。型付き配列は生成時に要素の数を指定する必要がありますが、それにはAnalyserNodeオブジェクトのfrequencyBinCountプロパティを使いましょう。

frequencyBinCountプロパティには、同じくAnalyserNodeオブジェクトのプロパティであるfftSizeの1/2の値が設定されています。fftSizeプロパティは、周波数ごとの波形の振幅を解析するメソッドが、どれだけ細かな周波数ごとに解析するかを示す値で、デフォルトでは2048に設定されています。この値は、アナログ波形のデジタル化粒度を表すサンプリング周波数に対応し、例えば2048である場合、0Hzからデフォルトのサンプリング周波数である44100Hzまでが、均等に2048等分されて解析されます。

ただし、サンプリング定理によると、サンプリング周波数の1/2以上のデジタル波形は、アナログ波形に復元不可能であり意味を持ちません。つまり、解析結果も半分まで、つまりfftSizeの値が2048の場合は1024個までしか意味を持たないということになります。

fftSizeの1/2の値であるfrequencyBinCountプロパティは、常にこの境界値を表しており、その値を型付き配列の要素数に指定すべき理由は、それ以上の解析結果が不要であるためです。

今回は、解析結果の全周波数の振幅から平均の振幅を求め、それを音量として利用します。

<p data-height="265" data-theme-id="0" data-slug-hash="vXLYVZ" data-default-tab="js" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160902" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/vXLYVZ/">160902</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

これで解析の準備がととのいました。
音源となるMediaStreamAudioSourceNodeをAnalyserNodeに接続して出力を開始させ、requestAnimationFrameを使って1フレームごとにHTMLへ音量を表示させてみましょう。

AnalyserNodeは中間処理の一つと言えますが、視覚化などに用いられるため、必ずしも出力が必要とは限りません。そのため、最終出力を表すAudioNodeではないにもかかわらず、別のAudioNodeへの出力が必須ではありません。

今回の場合も、音量の数値化が目的であり再生は必要ないため、AnalyserNode以降、最終出力には接続していません。

<p data-height="265" data-theme-id="0" data-slug-hash="bwENGz" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160903" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/bwENGz/">160903</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

周囲の音や声によって画面の数字が上下していますでしょうか。

取得した値は、このようにただ画面に表示させるだけでなく、CSSやJSの値として使うことももちろん可能です。

次にいくつかその実例を挙げてみます。

### 取得した音量の値をCSSの値に適用してみる

1つ目は、CSSのopacityに適用してみた例です。
消音状態では透明なSVGが、音を感知すると画面に現れます。

<p data-height="265" data-theme-id="0" data-slug-hash="WGxKvo" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160904-opacity" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/WGxKvo/">160904-opacity</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

2つ目は、CSSのcolorに適用してみた例です。
消音状態では何も起きませんが、音を感知するとSVGの色が変化します。

<p data-height="265" data-theme-id="0" data-slug-hash="kkXjkZ" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160904-color" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/kkXjkZ/">160904-color</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

3つ目は、CSSのtransform: rotate();に適用してみた例です。
消音状態では停止したSVGが、音を感知すると回転します。

<p data-height="265" data-theme-id="0" data-slug-hash="KgrBYZ" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160904-rotate" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/KgrBYZ/">160904-rotate</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## まとめ

今回は、マイクからの音声を音源として利用する方法と、音源を解析する方法をご紹介しました。再生、加工、生成、解析と、できることがどんどん増えてきてきましたね。

さて、これらを組み合わせて次は何を作ろうかな……。

ワクワクが止まらないつっちーでした。ではまた！

