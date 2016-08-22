把浏览器变成钢琴！Web Audio API入门
***

>* 原文链接 : [webブラウザがピアノになる！「Web Audio API」入門](http://liginc.co.jp/284679)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/07/eyecatch_160706_01_m.png)

web浏览器现在有各种二样、五花八门的功能，不乏一些比较有趣的，比如使用canvas元素的一些游戏与3DCG，使用WebRTC进行浏览器间的P2P通信等。

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
  距离到最终阶段为止很有可能有巨大的内容变化，“勧告”段階にない規格は、このことを認識した上で利用する必要があります。

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

| 作品名	| Berklee samples v.4 |
| 音源ファイル |	[https://archive.org/details/Berklee44v4](https://archive.org/details/Berklee44v4) |
| 原作者	| @metasj |

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

### 音の高さを変えてみる

AudioNodeには、自身の状態を表す可変の属性を持つものがあります。

今回使用しているAudioBufferSourceNodeも、自身の再生速度を表し、増減が可能な、playbackRate属性を持っています。再生速度を上下させることで周波数も増減するので、これを利用して音の高さを変えてみます。

AudioBufferSourceNodeのplaybackRate属性は、この属性の持つvalue属性を通して変更できます。変更していない状態を1として比率を設定し、再生速度を増減します。

```javascript
bufferSource.buffer = data;
// 再生速度を2倍に設定すると、周波数も2倍になり、音は高くなる
bufferSource.playbackRate.value = 2;
bufferSource.connect(ctx.destination);
bufferSource.start(0);
```

再生速度が速くなると周波数も同じ比率で大きくなるため、音が高くなります。

```javascript
bufferSource.buffer = data;
// 再生速度を半分に設定すると、周波数も半分になり、音は低くなる
bufferSource.playbackRate.value = 0.5;
bufferSource.connect(ctx.destination);
bufferSource.start(0);
```

再生速度が遅くなると、周波数も同じ比率で小さくなるため、音は低くなります。

これをレンジバーで変更できるようにしたものが、こちら。

[源代码](https://github.com/lig-dsktschy/waapi-piano/tree/gh-pages/playbackrate)

[サンプル](http://lig-dsktschy.github.io/waapi-piano/playbackrate/)

音が変わりました！

### ピアノっぽくしてみる

では、いよいよピアノっぽくしていきましょう。

今回は、音の高さの変更に再生速度の変更を利用しますが、この方法では音質も変化してしまいます。この音源の場合、高くしたときの音質変化が特に耳につくため、低くするのみで音の高さを変更していきます。

まずHTMLとCSSで鍵盤を作ります。今回使用している音源は、C（ド）の音です。
音の高さは低くするのみと決めたので、このC（ド）が一番高い音、つまり右端の鍵盤がC（ド）となるように、白鍵と黒鍵をならべます。

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
 
// 鍵盤要素の集合を配列化する
var keyboards = Array.prototype.slice.call(
    document.getElementsByClassName('keyboard')
);
// 右端から逆順に、鍵盤ごとの処理をしていく
keyboards.reverse().map(function(keyboard, index) {
     
    // 鍵盤ごとの処理
 
});
```

右端の鍵盤C（ド）を計算の基準とするため、右から左へ向かって逆順に、鍵盤ごとの処理をしていきます。

ピアノ（平均律）においては、ある音とその右隣の音との周波数比は、1：約1.059463となります。つまり、ある音とその左隣の音との周波数比は、約1.059463分の1：1となります。

これを利用して、鍵盤ごとに、右端の鍵盤C（ド）との周波数比を計算します。

```javascript
// 平均律における、ある音の隣の音に対する周波数比(近似値)
var frequencyRatioTempered = 1.059463;
 
// 〜 省略 〜
 
keyboards.reverse().map(function(keyboard, index) {
    // 基準のC（ド）から何音はなれているかで、周波数比を求める
    var frequencyRatio = 1;
    for (var i = 0; i < index; i++) {
        frequencyRatio /= frequencyRatioTempered;
    }
}
```

前項で説明した通り、周波数と再生速度は同じ比率で増減するため、上で算出した周波数比を、そのまま再生速度比として設定します。

```javascript
bufferSource.buffer = data;
bufferSource.playbackRate.value = frequencyRatio;
bufferSource.connect(ctx.destination);
bufferSource.start(0);
```

これらをまとめたものが下記になります。
[源代码](https://github.com/lig-dsktschy/waapi-piano/tree/gh-pages/piano)

[demo](http://lig-dsktschy.github.io/waapi-piano/piano/)

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/06/piano.gif)

ピアノっぽいですね！ 完成です！！

