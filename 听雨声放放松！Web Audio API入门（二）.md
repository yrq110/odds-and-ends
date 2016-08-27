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

* 适合音源
  短音源

  （例：钢琴与打击乐器等单次音源）

  获得音频数据时，需要等待全部数据解码完成才能使用，与长音源相反。

* 适合的使用场景
  需要控制发声时刻的场合

  （例：游戏的効果音）

* 其它特点
  由于对象是一次性的，播放后需要重新生成。

### MediaElementAudioSourceNode

* 适合音源
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
    // AudioContextを生成
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
// 连接表示音源的音源AudioNode与表示最终输出的
mediaElementSource.connect(ctx.destination);
// 事件注册
var isPlaying = false;
elButton.addEventListener('click', function() {
    elAudio[!isPlaying ? 'play' : 'pause']();
    isPlaying = !isPlaying;
});
```
