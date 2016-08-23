#把浏览器变成钢琴！Web Audio API入门

***

>* 原文链接 : [webブラウザがピアノになる！「Web Audio API」入門](http://liginc.co.jp/284679)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/07/eyecatch_160706_01_m.png)

web浏览器现在有各种各样、五花八门的功能，不乏一些比较有趣的，比如使用canvas元素的一些游戏与3DCG，使用WebRTC进行浏览器间的P2P通信等。

在那其中，对音频的操作在最近引起了我的兴趣。那么今天就来说说在web浏览器上处理音频的「WebAudioAPI」。

## 所谓「WebAudioAPI」？

> “a high-level JavaScript API for processing and synthesizing audio in web applications” 
----[Web Audio API – W3C](https://www.w3.org/TR/2015/WD-webaudio-20151208/#abstract)

翻译过来就是「为处理与合成音频的web应用所准备的高级JavaScript API」。

## 三个使用「Web Audio API」的示例网站

### Javascript Drone

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/07/waa011.png)

[http://matt-diamond.com/drone.html](http://matt-diamond.com/drone.html)

播放令人舒服的嗡嗡声(持续的声音)。通过调整Base Note与Number of Generators两个参数来调整声音，可以进行音频文件的录制与下载。

### HTML5 Drum Machine

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/06/waa02.png)

[http://www.html5drummachine.com](http://www.html5drummachine.com/)

一台鼓机，设置不同乐器的发音时间，自动进行电子鼓的演奏。可以改变节拍(Tempo)与音色类型，同样可以进行音频文件的录制与下载。

### Loop Waveform Visualizer(PS:这个很酷炫)

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/06/waa03.png)

[https://airtightinteractive.com/demos/js/reactive](https://airtightinteractive.com/demos/js/reactive)

将音乐可视化的工具。将mp3文件拖入界面中，或者点击「load sample mp3」开始播放示例音乐，各种颜色的波纹，配合音乐不断振动不断扩大。

这些全部是使用「Web Audio API」在web浏览器上实现的！是不是有一些想法了，这次的目标是作出一个可以在web浏览器上弹的钢琴，首先从产生声音开始吧。

## 使用「Web Audio API」之前

开始使用Web Audio API之前，有两个需要注意的地方。

1. WebAudioAPI处于W3C发布标准的“工作草案（Working Draft）”阶段（2016年6月）
  距离到最终阶段为止很有可能有巨大的内容变化。

  参考:[https://www.w3.org/TR/#tr_Audio](https://www.w3.org/TR/#tr_Audio)
2. 不支持 Internet Explorer 11
  Web Audio API不支持IE11与Android4.4以下的自带的浏览器，支持Edge, Android版Chrome。

  参考:[http://caniuse.com/#feat=audio-api](http://caniuse.com/#feat=audio-api)

能尽快无所顾虑的使用就好了...

## 使用「Web Audio API」在浏览器中制作钢琴

那么现在开始吧~

### 产生声音

Web Audio API以AudioContext为主，衍生出表示音源、中间处理、最终输出等的AudioNode。

```javascript
// 初始化AudioContext
var ctx = new AudioContext();
 
// 从AudioContext中生成AudioNode
// AudioBufferSourceNode: 处理一次性短音的AudioNode
var bufferSource = ctx.createBufferSource();
```

对于音源、中间处理与最终输出等，根据细分出的不同内容，都有对应的继承自AudioNode的对象，并且AudioNode具有与其他AudioNode对象相连接的connect方法。

```javascript
// 保存音源
bufferSource.buffer = data;
 
// 与最后输出的音源连接
// AudioDestinationNode: 表示最后的输出
//   可以参考AudioContext的destination属性
bufferSource.connect(ctx.destination);
 
// 播放音源
bufferSource.start(0);
```

如例子所示，将表示音源的AudioNode与表示最终输出的AudioNode相连接，就准备好播放音源了。在这次的应用中，不进行任何中间处理，直接将音源与最终输出连接起来使用。

使用短音来模拟钢琴键盘的单次音效。

| 条目 | 内容 |
| ------------- |-------------| 
| 作品名	| Berklee samples v.4 |
| 音源文件 |	[https://archive.org/details/Berklee44v4](https://archive.org/details/Berklee44v4) |
| 原作者	| [@metasj](https://archive.org/details/@metasj) |

```javascript
// 获取指定音源文件的二进制数据
var xml = new XMLHttpRequest();
xml.responseType = 'arraybuffer';
xml.open('GET', 'media/piano.wav', true);
xml.onload = function() {
    // 获取二进制数据并解码
    ctx.decodeAudioData(
        xml.response,
        function(_data) {
            data = _data;
        },
        function(err) {
            // error
        }
    );
};
```

处理短音源的AudioNode很适合作为AudioBufferSourceNode，因为一次性使用后不能再次利用的部分，为了释放内存会被立即释放。

一般情况下AudioBufferSourceNode使用的是从二进制数据解码得到的音源，可以使用XHRHttpRequest来获取音源的二进制数据。

组合这些代码，在画面上点击时会有声音。

[GitHub源代码](https://github.com/lig-dsktschy/waapi-piano/tree/gh-pages/play)

[demo](http://lig-dsktschy.github.io/waapi-piano/play/)

声音响啦！

### 改变音调

AudioNode有可以改变自身状态的可变属性。

这次使用的AudioBufferSourceNode，有一个可以改变自身播放速度的playbackRate属性，加快或减慢播放速度时声音的频率会随着改变，利用这个来改变声音的音调。

通过AudioBufferSourceNode的playbackRate属性的value值来增减播放速度，不改变的情况下设定为1。

```javascript
bufferSource.buffer = data;
// 设定为2倍的播放速度，频率会变为之前的2倍，音调会升高
bufferSource.playbackRate.value = 2;
bufferSource.connect(ctx.destination);
bufferSource.start(0);
```

由于加快播放速度时，频率会随其等比例增大，因此音调会升高。

```javascript
bufferSource.buffer = data;
// 设定为0.5倍的播放速度，频率会变为之前的一般，音调会降低
bufferSource.playbackRate.value = 0.5;
bufferSource.connect(ctx.destination);
bufferSource.start(0);
```

由于减慢播放速度时，频率会随其等比例减小，因此音调会降低。

在下面这个例子中可以在一定范围内改变音调。

[源代码](https://github.com/lig-dsktschy/waapi-piano/tree/gh-pages/playbackrate)

[demo](http://lig-dsktschy.github.io/waapi-piano/playbackrate/)

音调变化了！

### 弹奏钢琴

那么是时候来弹奏钢琴了。

利用播放速度的改变来调整音调，使用这个方法时也会改变音质，由于频率较高时音质变得特别刺耳，因此我们需要降低一下音调。

首先使用HTML与CSS来制作键盘，这次使用的音源是C（do）音。

决定了降低音调后，将这个C音作为最高的音，也就是键盘最右端的C，其余按顺序摆放白键与黑键。

HTML:
```html
<ul>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-black"></li>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-black"></li>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-black"></li>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-black"></li>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-black"></li>
    <li class="keyboard keyboard-white"></li>
    <li class="keyboard keyboard-white"></li>
</ul>
```

CSS:
```css
html, body, ul, li {
    box-sizing: border-box;
}
html, body, ul {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
li {
    list-style: none;
}
.keyboard {
    transition: background-color .1s ease 0s;
}
.keyboard:active {
    background-color: #DFFF30;
}
.keyboard-white {
    float: left;
    width: calc(100% / 8);
    height: 100%;
    border: 1px solid black;
}
.keyboard-black {
    height: 60%;
    position: absolute;
    top: 0;
    width: calc(100% / 12);
    background-color: black;
    border: 2px solid black;
}
.keyboard:nth-of-type(2) {left: 8%}
.keyboard:nth-of-type(4) {left: 21%}
.keyboard:nth-of-type(7) {left: 45%}
.keyboard:nth-of-type(9) {left: 58%}
.keyboard:nth-of-type(11) {left: 71%}
```

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/06/piano.png)

```javascript
var isSP = typeof window.ontouchstart !== 'undefined';
 
// 将所有键整合成数组
var keyboards = Array.prototype.slice.call(
    document.getElementsByClassName('keyboard')
);
// 从右向左来依次处理键盘上的键
keyboards.reverse().map(function(keyboard, index) {
     
    // 处理键
 
});
```

以最右端的C为基准，从右往左来处理每个键的音调。

钢琴是以平均律为基础的，每个音与右邻音的频率比例大约为1：1.059463，与左邻音的频率比例大约为1.059463：1。

利用这个来计算每个音调与最右端C音的音调频率比。

```javascript
// 根据平均律得出的相邻音调之间的频率比(近似値)
var frequencyRatioTempered = 1.059463;
 
// 〜 省略 〜
 
keyboards.reverse().map(function(keyboard, index) {
    // 根据基准音C求得其他音调相对于它的频率比例
    var frequencyRatio = 1;
    for (var i = 0; i < index; i++) {
        frequencyRatio /= frequencyRatioTempered;
    }
}
```

前面已经说过，频率与播放速度时同比增减的，因此直接将上面算出的频率比设定为播放速度。

```javascript
bufferSource.buffer = data;
bufferSource.playbackRate.value = frequencyRatio;
bufferSource.connect(ctx.destination);
bufferSource.start(0);
```

接下来是总结。

[源代码](https://github.com/lig-dsktschy/waapi-piano/tree/gh-pages/piano)

[demo](http://lig-dsktschy.github.io/waapi-piano/piano/)

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/06/piano.gif)

钢琴可以弹了唉╮(╯▽╰)╭！ 完成搞定！


## 与audio元素的不同

使用HTML5中新增的audio元素来播放音源也可以实现，不过有一些不同:

* 根据浏览器的不同对同时发声的个数有限制
* 不能进行音源播放之前的中间处理

## 总结

这次使用Web Audio API做出了一个可以弹奏钢琴的应用。在浏览器上就可以演奏是不是挺棒？用手机访问的话，可以进行2指与3指的和弦演奏，请务必尝试一下(PS:我用iOS的Chrome试了下不行...)。

那么回见！
