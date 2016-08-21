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
