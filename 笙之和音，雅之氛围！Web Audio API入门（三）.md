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

作为和音演奏中的主要乐器，吹与吸均能产生声音，可以发出持续时间较长的声音。

乐器形状好像一只收翼休憩的凤凰，音色犹如透过天际的光芒，非常优美。

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

为了有点演奏的感觉，使用点击或触摸操作来控制声音的播放。

<p data-height="265" data-theme-id="0" data-slug-hash="YWmOGq" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160806" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/YWmOGq/">160806</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

是不是有点乐器的感觉了？

下面来产生和音。

### 制作和音

首先整理出笙所发出声音频率。

这种调音与十二平均律(参见上一篇文章)是不同的，可以参考下面这个站点。

> [笙吹きロバの笙の調律コーナー](http://gagaku.okunohosomichi.net/choritsu1.htm)

<p data-height="265" data-theme-id="0" data-slug-hash="yJmxXQ" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160807" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/yJmxXQ/">160807</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

下面构建笙的和音频率数组。

参考[Wikipedia](https://ja.wikipedia.org/wiki/%E7%AC%99#.E5.90.88.E7.AB.B9)，使用6个音就可构建和音的拾音器。

<p data-height="265" data-theme-id="0" data-slug-hash="JKgayo" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160808" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/JKgayo/">160808</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

由于每个OscillatorNode只能产生一种波形，使用多个OscillatorNode同时播放来实现和音效果。

设定构成和音6音的OscillatorNode频率，连接到最终的输出上。

<p data-height="265" data-theme-id="0" data-slug-hash="oLKPEx" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160809" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/oLKPEx/">160809</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

播放出和音了！

下面，我们将每次点击或触摸时发出的和音种类改为随机选择的结果。

<p data-height="265" data-theme-id="0" data-slug-hash="YWmOJk" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160810" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/YWmOJk/">160810</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

实际演奏时声音的开始与结束不会像上面的例子一样，一会儿是最大音量一会儿又突然没有声音，应该是一种平滑的变化。

也就是说，需要加入一种淡入(fade in)与淡出(fade out)的效果。

### 尝试淡入与淡出

AudioParam对象有一些可以根据时间值自动调整value属性与defaultValue属性等值的方法，被称为自动方法(AutomaticMethod)。

linearRampToValueAtTime是自动方法中的一种，操作value属性的值使其在一定时间内从当前值变化到设定值。

可以这样操作GainNode的gain属性来实现淡入·淡出。

WebAudioAPI将当前时刻的值保存在了AudioContext的currentTime属性中，单位为秒。

<p data-height="265" data-theme-id="0" data-slug-hash="qadaZw" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160811" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/qadaZw/">160811</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

使用linearRampToValueAtTime时，需要将value属性的当前值与当前时间结合起来，若未进行这个操作，属性值会没有变化的起点，立刻发生变化，产生与所设定内容不同的效果。

为了将value属性的当前值与当前时刻结合起来，需要使用同为自动方法的setValueAtTime方法。

setValueAtTime方法会将value属性的值在指定的时刻改为指定的值。

将方法的目标值设为value的当前值，改变时刻设为当前时刻，这样就完成绑定了。

由于使用当前值覆盖了当前值，因此看起来没有什么变化。

<p data-height="265" data-theme-id="0" data-slug-hash="xEGRdv" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160812" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/xEGRdv/">160812</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

接下来，需要考虑在淡入的过程中淡出或者在淡出的过程中淡入的情况下对应的措施。

这是因为有可能中途会执行其他方法，需要使之前的方法再次改变它的目标值，是意料之外的举动。

AudioParam对象的cancelScheduledValues方法是一种将未来的注册值全部取消的自动方法。

它需要在setValueAtTime之前执行，处理在事件发生过程中发生其他事件的情况。

<p data-height="265" data-theme-id="0" data-slug-hash="vXOyZK" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160813" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/vXOyZK/">160813</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

除此之外，还需要控制在中途进行的淡入·淡出时的执行时间，最后来处理这种情况。

<p data-height="265" data-theme-id="0" data-slug-hash="ZpGvoa" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160814" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/ZpGvoa/">160814</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

在这个页面上AudioContext已经物尽其用了！可以在[这里](http://sho.netlify.com/)看到最终的结果。

<p data-height="265" data-theme-id="0" data-slug-hash="akZRJp" data-default-tab="result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="1608-completed" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/akZRJp/">1608-completed</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

[运行结果](http://sho.netlify.com/)

背景会随着点击·触摸的动作变化，宛如...从天上射出的光芒？完成了！

### 总结

这次介绍了在浏览器上生成音源的方法。

除了四种基本波形以外，WebAudioAPI也可以生成自定义的波形与复杂的噪声。

虽然自定义音源比起现成的音源文件实现起来更加复杂，不过相对来说也更加自由。

请务必尝试一下。

那么回见！

