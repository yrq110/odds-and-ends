# 画随音动！Web Audio API入门（四）

***

>* 原文链接 : [音にあわせて画面が変化！続々々「WebAudioAPI」入門](https://liginc.co.jp/310761)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

这次介绍解析音源并可视化的方法。

> 请确保在阅读本文时，浏览器的其他标签或窗口没有在使用WebAudioAPI。
>
> Web浏览器对同时存在的AudioContext对象数量是有限制的。一般情况下一个应用不需要用到多个AudioContext对象，这个限制也就不会让人令人困惑了。不过有可能多个标签、窗口或iframe同时使用WebAudioAPI，这样就会发生错误，因此在阅读本篇文章时需要先终止其他地方的使用。

## 将音源数据解析后进行可视化的网站
### Loop Waveform Visualizer

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/06/waa03.png)

[https://airtightinteractive.com/demos/js/reactive](https://airtightinteractive.com/demos/js/reactive)

这个是之前介绍的将播放的音源可视化的网站。

将mp3文件拖拽到界面中，或者点击「load sample mp3」(加载示例音乐)开始播放。

这个网站使用WebAudioAPI解析音源每一时刻的音量，使用Three.js的圆形展现音量值的大小，实现可视化。

至今为止的文章都是介绍音频文件的操作，这次将操作的对象换成从麦克风得到的声音。

## 使用「Web Audio API」根据声音调整显示画面

### 使用麦克风的输入作为音源

声音与动画等的多媒体内容一般使用MediaStream对象，可以通过使用navigator.mediaDevices对象的getUserMedia方法来获得MediaStream对象。

要在WebAudioAPI操作MediaStream对象的话需要使用AudioNode中的MediaStreamAudioSourceNode。

> 使用getUserMedia的注意事项

使用getUserMedia时需要注意以下3点。

1. 不支持Safari(Mac/iOS)

  目前[Mac与iOS的Safari都未实现这个方法](http://caniuse.com/#search=getusermedia)。
2. 需要polyfill

  getUserMedia以前是navigator对象的一个方法(navigator.getUserMedia)，而现在不推荐这样做，目前所有的浏览器都是通过调用navigator.mediaDevices.getUserMedia来使用这个方法，准备了必要的polyfill。详情请参见[MDN](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)。
  [这里](https://github.com/lig-dsktschy/ligfes20160426/blob/gh-pages/01/js/getusermedia-commented.js)将MDN介绍中关于老版本浏览器使用getUserMedia的polyfill代码提取了出来，可以先看看。
3. 必须是HTTPS

  由于安全策略必须使用HTTPS访问才能正常使用getUserMedia，否则会失败。目前很多网站如GithubPages、CodePen、Netlify都提供了免费的HTTPS服务，直接使用HTTPS访问即可。
  如果配置个人证书的话比较复杂，还是使用上面的那几个站测试吧。

那么下面先将其连接到最终输出上吧。

点击RESULT按钮执行下面代码。

<p data-height="265" data-theme-id="0" data-slug-hash="jrbJGX" data-default-tab="js" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160901" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/jrbJGX/">160901</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

应该能听到周围的声音，会有一些延迟。

在从麦克风得到声音后会生成MediaStream对象，这个对象的数据是实时更新的。将生成的MediaStreamAudioSourceNode与其他AudioNode连接进行音频输出。

成功获得麦克风的输入声音后，接着要解析音源得到音量的值。

### 解析出音源的音量大小

使用AudioNode中的AnalyserNode来进行解析处理。

AnalyserNode具有几个解析音源的方法，由于这些方法执行结果的类型各不相同，需要准备对应类型的数组进行存储。

每个频率波的振幅为8bit的无符号整数，即0~255。使用getByteFrequencyData方法可以直接将数据存储在参数中指定的数组。

由于执行得到的结果是无符号的8bit整数，要存储在类型为Uint8Array的数列中，生成类型数组时还必须制定其中的元素个数，可以使用AnalyserNode对象的frequencyBinCount属性。

frequencyBinCount属性应设为AnalyserNode对象的另一个属性fftSize值的一半。fftsize属性的值表示解析频率波振幅的方法要将波形分的有多细，若这个值较大，那么解析后的每一部分就很小，默认值为2048，它表示模拟信号转化为数字信号时的颗粒数量，对应采样频率，比如说当它为2048时，根据默认的采样频率会将从0Hz到44100Hz的部分解析为均等的2048份。

不过根据奈奎斯特采样定理，若数字信号的频率大于采样频率的一半则不能还原为模拟信号，因此只有一半的解析结果是有意义的，可以使用的。

frequencyBinCount属性的值一般为fftSize值的一半，这个值是临界值，至于为何要使用这个值作为类型数组的元素个数，根据上述理由，除了这些数量外的信号是没有意义的。

解析结果为所有频率声波的振幅的平均值，将其作为音量的大小。 

<p data-height="265" data-theme-id="0" data-slug-hash="vXLYVZ" data-default-tab="js" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160902" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/vXLYVZ/">160902</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

这样就做好解析的准备了。

将音源MediaStreamAudioSourceNode与AnalyserNode连接起来，使用requestAnimationFrame的每一帧来表示音量并通过HTML标签展现。

AnalyserNode相当于一个中间处理，用于数据的可视化，因此它的音源输出可有可无，将它连接到表示最终输出的AudioNode上也并不是必须的。

由于这次的目的是进行音量的数值化，不需要播放声音，因此就不用将AnalyserNode连接到最终输出上了。

<p data-height="265" data-theme-id="0" data-slug-hash="bwENGz" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160903" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/bwENGz/">160903</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

可以观察到，根据周围的声音变化画面中的数字会上下变动吧。

除了将取得的音量值这样表示出来，也可以结合CSS与JS属性进行操作。

下面列举几个例子。

### 将音量值与CSS属性值结合

第一个例子是用在CSS的opacity属性上。

静音时为透明的SVG，检测到声音后出现画面。

<p data-height="265" data-theme-id="0" data-slug-hash="WGxKvo" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160904-opacity" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/WGxKvo/">160904-opacity</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

第二个例子是用在CSS的color属性上。

静音时什么都不会发生，检测到声音后SVG的颜色会发生变化。

<p data-height="265" data-theme-id="0" data-slug-hash="kkXjkZ" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160904-color" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/kkXjkZ/">160904-color</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

第三个例子是用在CSS的transform: rotate();变换。

静音时为静止的SVG，检测到声音后开始旋转。

<p data-height="265" data-theme-id="0" data-slug-hash="KgrBYZ" data-default-tab="js,result" data-user="lig-dsktschy" data-embed-version="2" data-pen-title="160904-rotate" class="codepen">See the Pen <a href="http://codepen.io/lig-dsktschy/pen/KgrBYZ/">160904-rotate</a> by ligdsktschy (<a href="http://codepen.io/lig-dsktschy">@lig-dsktschy</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 总结

这次介绍了从麦克风获取音源与解析音源的方法。播放、加工、生成、解析，可以做的事情越来越多了呢。

将这些组合起来下次会做些什么呢……。

已经迫不及待了吧，那么回见！

