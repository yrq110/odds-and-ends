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

这个是以前介绍过的可以播放嗡嗡声的网站。

このドローンは複数の音源を同時発音することで表現されていて、その音源はWebAudioAPIを用いてブラウザ上で生成されています。
这次同样使用WebAudioAPI来生成音源，制作一个雅乐所使用的乐器——笙的声音。

## 使用「Web Audio API」在Web浏览器上产生笙的声音

### 笙是什么乐器？

「雅楽」は、お正月などに耳にしたことがあるかと思います。
その中でもひときわ神秘的な雰囲気を醸し出している、ミャーという音、あれが笙です。

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

### 重拾丢弃过的对象

OscillatorNodeは、AudioBufferSourceNode(前回、前々回記事参照)と同じく、使い捨てのオブジェクトであるため、一度停止した後は再生することができません。

今回のように時間経過による変化がない音源を使用する場合、GainNode(前回記事参照)によって音量を0に切り替えることで、停止を代用することができます。

<p data-height="265" data-theme-id="0" data-slug-hash="xOvaxN" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160805" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/xOvaxN/">160805</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

ただ、この停止方法では、聞こえていないだけで、再生は音量を0にしても続いています。楽曲のように時間経過によって音源の状態が変化していく場合、この停止方法では停止直前と再生直後とで音源の状態が繋がらないため、注意が必要です。

より演奏している感覚に近付けるため、クリック・タッチしている間だけ再生されるようにしてみましょう。

<p data-height="265" data-theme-id="0" data-slug-hash="YWmOGq" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160806" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/YWmOGq/">160806</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

ちょっと楽器感が出てきたのではないでしょうか？
次は和音を発生させてみます。
