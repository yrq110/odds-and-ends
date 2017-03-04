# 使用Web Audio Editor进行更直观的开发！Web Audio API入门（五）

***

>* 原文链接 : [使用Web Audio Editor进行更直观的开发！Web Audio API入门（五）
](https://liginc.co.jp/322853)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/01/148481536457291800_80-1310x874.jpg)

不知不觉已经到（五）了。

这次介绍一下Firefox中用于WebAudioAPI辅助开发的工具-「Web Audio Editor」。

## 「Web Audio Editor」是什么？

Web Audio Editor是Firebox浏览器所提供的一个WebAudioAPI辅助开发的工具(至2016年11月时还没有其他浏览器提供类似的功能，我觉得当Web Audio API成为W3C的推荐标准时，其他浏览器应该也会具备这个功能吧)。

使用这个工具可以看到AudioNode的连接状态、拥有的AudioNode与各AudioParam对象的value属性。

## 使用「Web Audio Editor」
### 打开「Web Audio Editor」

首先打开Firefox。

Web Audio Editor是Firefox浏览器开发工具中的一部分。因此打开Firefox后先打开开发工具。

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/01/148481503268393000_29.png)

Windows下使用ctrl + shift + I快捷键，MacOSX下使用command + option + I快捷键。

由于默认是禁用Web Audio Editor的，需要在开发工具的设置里勾选上「Web Audio」（译者注:中文版的火狐浏览器中这个选项为「网络音频」）。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147822815299567000_66.png)

这样在标签栏中就有「Web Audio」了，可以正常使用Web Audio Editor了。

选中标签栏中「Web Audio」会有一个过渡页面，会对过渡前页面的AudioContext进行验证。若已经对当前页的AudioContext进行验证过了，就不用再次载入了。
