#听听雨声放放松！Web Audio API入门（二）

***

>* 原文链接 : [雨音でリラックス！続「Web Audio API」入門](https://liginc.co.jp/293921)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/08/147195967181872800_47.jpg)

[上一次](https://github.com/yrq110/OddsAndEnds/blob/master/%E6%8A%8A%E6%B5%8F%E8%A7%88%E5%99%A8%E5%8F%98%E6%88%90%E9%92%A2%E7%90%B4%EF%BC%81Web%20Audio%20API%E5%85%A5%E9%97%A8.md)我们使用WebAudioAPI制作了一个Web浏览器中的钢琴。

在大家的浏览器上可以正常演奏吧。

在钢琴的实现中将音源与最终输出直接连接了起来，这次来试试中间处理吧。

中间处理可以说是WebAudioAPI的功能中与HTML的Audio元素相比区别最大的部分了。

# 持续播放雨声的网站

有一些公开的Web站点，持续播放作为放松与集中精神的BGM的连绵的下雨声。

比如说下面这个。

## Rainy Mood

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/07/rainymood.png)

[http://www.rainymood.com/](http://www.rainymood.com/)

下着阴郁的雨的天气，仅仅听着这样的声音是否觉得挺舒服的？

这次使用WebAudioAPI的中间处理，在像这样的雨声播放功能的基础上增加了音质变化。

# 使用「Web Audio API」制作播放雨声的网站

## AudioBufferSourceNode与MediaElementAudioSourceNode

在利用音频文件作为音源的AudioNode中，除了上次使用的AudioBufferSourceNode以外，还会使用MediaElementAudioSourceNode。

根据不同的适用音源与使用场景选择不同的AudioNode是很必要的。

### AudioBufferSourceNode

* 适合的音源
  短音源

  （例：钢琴与打击乐器等单次音源）

  获得音频数据时，需要等待全部数据解码完成才能使用，与长音源相反。

* 适合的使用场景
  需要控制发声时刻的场合

  （例：游戏的効果音）

* 其它特点
  由于对象是一次性的，播放后需要重新生成。

### MediaElementAudioSourceNode

* 适合的音源
  长音源
  
  （例：乐曲的音源、持续数十秒的音源）
  
  无需等待获取全部数据就可以开始播放。

* 适合的使用场景
  不注重准确的发生时刻，循环中不断播放的场合。

  （例：BGM）

  仅支持PC的场合。

  一些手机的浏览器也许可以控制audio元素，但并没有WebAudioAPI的相关功能。

* 其它特点
  生成对象后可以反复使用。
 

这一次使用持续较长时间的雨声作为音源。

* 作品名:Rain-Real_Ambi02-1
* 音源文件:http://musicisvfr.com/free/se/weather01.html
* 作者名:Music is VFR

需要不停的持续播放，根据这种情况选择MediaElementAudioSourceNode比较合适。

不过，对于那些不支持MediaElementAudioSourceNode的手机浏览器来说，就很遗憾了。

## 首先发出声音


MediaElementAudioSourceNode，顾名思义，需要将HTML的audio与video元素作为音源来使用。在作为MediaElementAudioSourceNode音源的使用时，也可以使用audio与video元素原本的功能。

也就是说，播放、停止与循环、自动播放等功能，与单独使用audio/video元素时同样的操作。使用WebAudioAPI的中间处理给audio/video元素的音频加特效——这么想的话比较容易理解。

HTML
```html
<audio src="media/rain.mp3" id="audio" preload="auto" loop></audio>
```
JS
```javascript
var
    // 初始化AudioContext
    ctx = new AudioContext(),
    // 获得audio元素
    elAudio = document.getElementById('audio'),
    // 从AudioContext生成AudioNode
    // MediaElementAudioSourceNode: 将audio/video元素作为音源操作的AudioNode
    mediaElementSource = ctx.createMediaElementSource(elAudio);
```

首先与上次一样，直接与最终输出连接，播放一下试试！

与AudioBufferSourceNode不同，可以反复使用初次生成的AudioNode。使用audio元素的播放/停止命令来控制MediaElementAudioSourceNode的播放/停止。

HTML
```html
<button id="button">Play / Stop</button>
```
JS
```javascript
// 连接表示音源的AudioNode与表示最终输出的AudioNode
mediaElementSource.connect(ctx.destination);
// 事件注册
var isPlaying = false;
elButton.addEventListener('click', function() {
    elAudio[!isPlaying ? 'play' : 'pause']();
    isPlaying = !isPlaying;
});
```

把上面的代码整合一下，加个下雨的背景图片。如下

[源码（GitHub）](https://github.com/lig-dsktschy/waapi-rain/tree/gh-pages/gain)

[demo](https://lig-dsktschy.github.io/waapi-rain/gain/)

雨下起来了唉O(∩_∩)O~~！不过这并没有进行中间处理，仅仅是使用audio元素进行播放而已。

那么是时候来让音量和音质变化了。

## 变化音量

表示中间处理的AudioNode有很多，其中的属性是表示自身处理状态的，继承自AudioParam的对象。

AudioParam对象，有表示处理状态的balue属性，表示value初始值的defaultValue属性，还有其他各种方法。这些属性与方法对于继承自AudioParam的所有对象来说都可以进行操作。

不过需要注意的是继承自AudioParam的对象名称与AudioNode是不同的。

表示调整音量的AudioNode是**GainNode**。GainNode中的gain属性是继承自AudioParam的对象。

gain对象的defaultValue值为1，value属性的设定为在0与1间的浮点数，0表示静音，1表示原始音量，可以重载音量大小。

```javascript
// 从AudioContext生成GainNode
// GainNode: 中间处理（调整音量）AudioNode
gain = ctx.createGain();
// 设定GainNode，对其连接的音源进行音量减半的处理
gain.gain.value = 0.5;
```

将GainNode与表示音源与最终输出的AudioNode相连接，就做好了以所设定的音量来播放音源的准备了。

```javascript
// 表示音源的AudioNode与表示中间处理(调整音量)的AudioNode连接
mediaElementSource.connect(gain);
// 表示中间处理的AudioNode与表示最终输出的AudioNode连接
gain.connect(ctx.destination);
```

在滑杆(范围选择控件)上进行音量调节。如下

[源码（GitHub）](https://github.com/lig-dsktschy/waapi-rain/tree/gh-pages/gain)

[demo](https://lig-dsktschy.github.io/waapi-rain/gain/)

可以调节成一场安静的雨！


# 複数の中間処理を挟んでみる

中间处理时可以进行多次连接。加上音量的调节后，也可以调整音质，使用低通滤波器与高通滤波器进行处理。

低通滤波器会滤掉比设定的频率值高的波，使低于设定值的波通过。高通滤波器则会滤掉比设定的频率值低的波，使高于设定值的波通过。

使用叫做BiquadFilterNode的AudioNode可以进行这些处理。

```javascript
// 从AudioContext生成BiquadFilterNode
biquadFilter = ctx.createBiquadFilter();
```

BiquadFilterNode通过改变type属性可以对多种文件进行处理。

type属性的值为字符串，’lowpass’对应低通滤波器，、’highpass’对应高通滤波器。

也可以设定为其他字符串，这个只使用效果比较容易理解的这两个。

```
// 设定BiquadFilterNode进行低通滤波器的处理
biquadFilter.type = 'lowpass';
```

BiquadFilterNode有多个继承自AudioParam的对象，其中的frequency属性可以设定截止频率(単位：Hz)。

frequency对象的defaultValue属性为350，value属性最小值为10，最大值为音源采样频率的一半(PS:应该是根据奈奎斯特抽样定律)。

```
// BiquadFilterNode会发挥低通滤波器的功能，除去1000Hz频率以上的波
biquadFilter.frequency.value = 1000;
```

value属性的范围与前文所述，不能将这个范围以外的数字信号解调成模拟信号，并且这个范围不会超出人的听力范围(20~20000Hz)太多。

可以通过文件属性来确认音源采样速率，一般设定为44100Hz。

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/07/samplerate.png)

将这BiquadFilterNode与表示音源的AudioNode与表示最终输出的AudioNode相连接。这样一来，给播放的音源添加滤波器的处理就准备完成了。

```
// 表示音源的AudioNode与表示音量调节处理的AudioNode连接
mediaElementSource.connect(gain);
// 表示音量调节处理的AudioNode与表示滤波处理的AudioNode连接
gain.connect(biquadFilter);
// 表示滤波处理的AudioNode与表示最终输出的AudioNode连接
biquadFilter.connect(ctx.destination);
```

可以通过选择列表与滑杆来调节以上属性，如下。

[源码（GitHub）](https://github.com/lig-dsktschy/waapi-rain/tree/gh-pages/biquad)

[demo](https://lig-dsktschy.github.io/waapi-rain/biquad/)

在这个demo的源码中使用了disconnect方法，可以中断AudioNode之间的连接。

可以中断与参数中所指定的AudioNode的连接，在这里没有进行指定，中断了全部连接。

使用connect方法连接的AudioNode若没有用disconnect方法显在的中断连接的话会一直连接在一起，这是为了使一个AudioNode能与多个AudioNode进行连接。

在这个例子中：

* BiquadFilter关闭时：
  GainNode → 最终输出
* BiquadFilter设定为低通或高通滤波器时：
  GainNode → BiquadFilterNode → 最终输出

因此使用它们可以调整AudioNode之间的连接。

```c#
// 同时中断GainNode与BiquadFilterNode的连接
gain.disconnect();
biquadFilter.disconnect();
// BiquadFilter关闭时
if (text === 'off') {
    // GainNode → 最终输出
    gain.connect(ctx.destination);
// BiquadFilter设定为低通或高通滤波器时
} else {
    // GainNode → BiquadFilterNode → 最終出力
    gain.connect(biquadFilter);
    biquadFilter.connect(ctx.destination);
}
```

这样，不仅加上了音量调节，也可以进行雨声音质的调整，调出低沉与清脆的声音。搞定！！

# 总结

这次对雨声进行了类似拾音器的中间处理，比较容易理解，也可以对其它元素进行调整，比如延迟与发声方向等。

除此之外，如果把音源文件换成其它环境音与乐曲的话也具有同样的效果，请务必尝试一下。

那么回见！
