# 笙之和音，雅之氛围！Web Audio API入门（三）

***

>* 原文链接 : [笙（しょう）の和音でみやびな気分！続々「Web Audio API」入門](https://liginc.co.jp/307261)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/09/147365738566254500_06-1310x874.jpg)


大家好，我是前端工程师つっちー。

上次和上上次我们学习了如何使用音效文件作为音源进行操作。

* [把浏览器变成钢琴！Web Audio API入门](https://github.com/yrq110/odds-and-ends/blob/master/%E6%8A%8A%E6%B5%8F%E8%A7%88%E5%99%A8%E5%8F%98%E6%88%90%E9%92%A2%E7%90%B4%EF%BC%81Web%20Audio%20API%E5%85%A5%E9%97%A8.md)
* [听听雨声放放松！Web Audio API入门（二）](https://github.com/yrq110/odds-and-ends/blob/master/%E5%90%AC%E9%9B%A8%E5%A3%B0%E6%94%BE%E6%94%BE%E6%9D%BE%EF%BC%81Web%20Audio%20API%E5%85%A5%E9%97%A8%EF%BC%88%E4%BA%8C%EF%BC%89.md)

下面来试着使用WebAudioAPI生成音源吧。

> 请确保在阅读本文时，浏览器的其他标签或窗口没有在使用WebAudioAPI。

> Web浏览器对同时存在的AudioContext对象数量是有限制的。一般情况下一个应用不需要用到多个AudioContext对象，这个限制也就不会让人令人困惑了。不过有可能多个标签、窗口或iframe同时使用WebAudioAPI，这样就会发生错误，因此在阅读本篇文章时需要先终止其他地方的使用。

## 浏览器上播放与生成音源的网站

### Javascript Drone

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/07/waa011.png)

[http://matt-diamond.com/drone.html](http://matt-diamond.com/drone.html)

这是以前介绍过的可以播放嗡嗡声的网站。

这个嗡嗡的声音是用多个音源同时发声来实现的，它的音源是在浏览器上用WebAudioAPI生成的。

这次同样使用WebAudioAPI来生成音源，制作一个雅乐中所使用的乐器——笙的声音。

## 使用「Web Audio API」在Web浏览器上产生笙的声音

### 笙是什么乐器？

「雅乐」，是一般在新年或者祭祀时会听到的传统音乐。

其中有一种可以营造出神秘氛围的乐器 —— 那就是笙。	

合竹（あいたけ）と呼ばれる和音の演奏が中心で、吹いても吸っても音が出るため、音を長く持続できるそうです。
形は翼を立てて休んでいる鳳凰（ほうおう）に見立てられ、音色は天から差し込む光を表すのだとか。素敵ですね。

### 首先产生声音

这次使用AudioNode中可以产生周期波形的OscillatorNode制作音源。

<p data-height="265" data-theme-id="0" data-slug-hash="qNZywG" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160801" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/qNZywG/">160801</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

当空气震动时会听到声音。

空气的震动可以用波形来表示，常用的波形有正弦波、矩形波、三角波和锯齿波四种。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147243386027684500_05.png)
（Wikipediaより）

OscillatorNode可以产生4种波形，通过设置type属性来指定波形的种类。
* sine: 正弦波
* square: 矩形波
* triangle: 三角波
* sawtooth: 锯齿波

<p data-height="265" data-theme-id="0" data-slug-hash="vKoawO" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160802" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/vKoawO/">160802</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

声音的高低会根据波形的重复次数而变化。

速度较快波形重复次数较多则为高音，速度较慢波形重复次数较少则为低音。

一定时间内波形的重复次数被称为频率，频率的单位为Hz(赫兹)，表示每秒的重复次数。也就是说频率大则为高音，频率小则为低音。

OscillatorNode的frequency属性是继承了AudioParam的对象，表示频率。

frequency对象的defaultValue属性值为440(单位:Hz)，给value属性设置任意的浮点数可以覆盖默认的频率值。

<p data-height="265" data-theme-id="0" data-slug-hash="WxVKBE" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160803" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/WxVKBE/">160803</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

这次直接与最终输出连接播放声音波形。

<p data-height="265" data-theme-id="0" data-slug-hash="jAgvOk" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160804" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/jAgvOk/">160804</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

可以在浏览器上生成音源了(点击demo页面播放音源)！

播放后听到声音后，可以通过改变type属性，听听四种波形的音色有什么不同。我个人觉得锯齿波比较接近笙的音色。

也就是说，要将type属性设置为sawtooth。

### 继续使用一次性对象

由于OscillatorNode与AudioBufferSourceNode(参见之前的系列文章)一样都是一次性使用的对象，在停止后不能再次播放。

这次的情况是随着时间不会变化的音源，使用GainNode(参见之前的系列文章)将音量调到0当做停止。

<p data-height="265" data-theme-id="0" data-slug-hash="xOvaxN" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160805" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/xOvaxN/">160805</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

不过用这种停止方法的话，仅仅是听不到而已，音源还是在以音量为0的状态继续播放着。需要注意若乐曲是根据时间变化的话，使用这种停止的方法不会保持停止前的状态，与继续播放时的状态会有所不同。

为了有点演奏的感觉，使用点击操作来控制声音的播放。

<p data-height="265" data-theme-id="0" data-slug-hash="YWmOGq" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160806" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/YWmOGq/">160806</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

是不是有点乐器的感觉了？

下面来产生和音。

### 制作和音

まず、笙が出す音の周波数を、配列として列挙しましょう。
平均律(前々回記事参照)とは異なる調律がされているため、こちらのサイトを参考にさせていただきました。

> [笙吹きロバの笙の調律コーナー](http://gagaku.okunohosomichi.net/choritsu1.htm)

<p data-height="265" data-theme-id="0" data-slug-hash="yJmxXQ" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160807" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/yJmxXQ/">160807</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

次に、上で挙げた配列を用いて、笙の和音の構成もまた、配列として列挙します。
[Wikipedia](https://ja.wikipedia.org/wiki/%E7%AC%99#.E5.90.88.E7.AB.B9)を参考に、6音で構成される和音のみピックアップしました。

<p data-height="265" data-theme-id="0" data-slug-hash="JKgayo" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160808" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/JKgayo/">160808</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

OscillatorNodeは、1つにつき1つの波形しか発生させることができないため、和音は複数のOscillatorNodeを同時に再生させることで表現します。
和音を構成する6音分のOscillatorNodeを、それぞれの周波数に設定し、最終出力まで接続しましょう。


<p data-height="265" data-theme-id="0" data-slug-hash="oLKPEx" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160809" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/oLKPEx/">160809</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

和音を再生することができましたね！
さらに、クリック・タッチのたび和音の種類がランダムに選択されるようにしておきます。

<p data-height="265" data-theme-id="0" data-slug-hash="YWmOJk" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160810" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/YWmOJk/">160810</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

実際に演奏される際の音の入り、音の終わりは、上のサンプルのようにいきなり最大音量、いきなり無音というわけではなく、なめらかに音量が上下します。
ということで、仕上げにフェードイン・フェードアウトをつけてみましょう。
