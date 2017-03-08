# 使用Web Audio Editor更直观的开发！Web Audio API入门（五）

***

>* 原文链接 : [「Web Audio Editor」でより直感的なWeb Audio API開発を！ – 続々々々「Web Audio API」入門 ](https://liginc.co.jp/322853)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

* [把浏览器变成钢琴！Web Audio API入门](https://github.com/yrq110/odds-and-ends/blob/master/%E6%8A%8A%E6%B5%8F%E8%A7%88%E5%99%A8%E5%8F%98%E6%88%90%E9%92%A2%E7%90%B4%EF%BC%81Web%20Audio%20API%E5%85%A5%E9%97%A8.md)
* [听听雨声放放松！Web Audio API入门（二）](https://github.com/yrq110/odds-and-ends/blob/master/%E5%90%AC%E5%90%AC%E9%9B%A8%E5%A3%B0%E6%94%BE%E6%94%BE%E6%9D%BE%EF%BC%81Web%20Audio%20API%E5%85%A5%E9%97%A8%EF%BC%88%E4%BA%8C%EF%BC%89.md)
* [笙之和音，雅之氛围！Web Audio API入门（三）](http://yrq110.me/2017/02/18/20170218-sheng-chord-web-audio-api/)
* [画随音动！Web Audio API入门（四）](http://yrq110.me/2017/02/27/20170227-volume-web-audio-api/)

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

### 检查AudioNode的连接状态

在使用Web Audio API开发时，会使用AudioNode的connect方法将多个AudioNode连接起来。在操作大量AudioNode的场合下，有时需要根据条件切换AudioNode间的连接状态，这时就很难通过代码来掌握AudioNode之间的连接状态吧。

Web Audio Editor通过将AudioNode的连接状态可视化来解决这个问题。

来实际操作下Web Audio Editor检查连接状态吧。

首先看看将表示音源的AudioNode连接到表示最终输出的AudioNode上的[demo](https://lig-dsktschy.github.io/wpapi-osc/1/)(点击链接前注意播放音量)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823213859569600_70.png)

每个AudioNode都用一个框表示，并使用一个箭头连接线表示执行connect方法的AudioNode与目标AudioNode之间的连接。

下面来看看同时输出多个音源的[demo](https://lig-dsktschy.github.io/wpapi-osc/2/)(点击链接前打开声音)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823215716495900_11.png)

所有表示音源的AudioNode都连接到了表示最终输出的AudioNode上，使用框图与带箭头的连接线表示。

那么如果连接到输出的音源变化时怎么办呢，来看看这个使用按键控制连接的[demo](https://lig-dsktschy.github.io/wpapi-osc/3/)(点击链接前打开声音)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823217765772200_99.png)

在表示AudioNode的方框间，在连接前没有箭头连接线。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823220931717800_67.png)

在连接时出现了箭头连接线。

像这样在Web Audio Editor中可以实时可视化的表示AudioNode的连接状态。

### 检查AudioParam对象

在使用Web Audio API开发时，不仅要操作AudioNode，也要操作AudioNode所持有的AudioParam对象，当代码与操作的AudioNode更加复杂时，要把握这些对象与属性就比较困难了。 

Web Audio Editor通过将所有AudioParam对象的值属性全部列出来解决了这个问题。

请实际操作下，使用Web Audio Editor查看AudioParam对象的值属性。再看看刚才的那个同时播放多个音源的[demo](https://lig-dsktschy.github.io/wpapi-osc/2/)(点击链接前打开声音)，这次请点击一下表示AudioNode的方框。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823224650594300_42.png)

点击AudioNode后框体会变为蓝色，并且出现了属性栏。

在属性栏这里可以看到AudioNode所拥有的AudioParam对象的值，图中所显示的是OscillatorNode的type, frequency, detune三个属性的值。

点击其它AudioNode的方框可以看到它们的frequency属性值。

那么改变AudioParam对象的属性值会有什么效果呢，看看这个添加了进度条调整音量的[demo](https://lig-dsktschy.github.io/wpapi-osc/4/)(点击链接前打开声音)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823226271241100_56.png)

点击表示中间处理的AudioNode即可查看它的值属性。如上图，可以看到GainNode的gain属性值。

下面，记住当前的gain值，然后调整进度条来改变属性值，再次点击Gain方框，应会看到此时的gain值是调整后的更新值。

这是由于Web Audio Editor将AudioParam对象的属性值更新为当前状态的值，不过与显示AudioNode连接状态不同的是，这个不是实时表现的。

AudioParam对象的属性值是在点击方框后更新成了当前值。 

## 总结

使用Web Audio Editor不仅可以检查自己所做的页面，也可以观察其他页面的Web Audio API相关使用情况。

在分析使用Web Audio API开发的页面时，善用Web Audio Editor着实可以帮不少忙。

那么回见！
