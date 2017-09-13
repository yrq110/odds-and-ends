# 快速检视效果！三种CSS生成器介绍

***

> * 原文链接 : [CSSを視覚的に素早く確認する！CSSジェネレーター・便利ツール3選](https://liginc.co.jp/364780)
> * 原文作者 : [ハル](https://liginc.co.jp/member/member_detail?user=hal)
> * 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/08/15041700444124700_35-1310x874.png)

大家好我是码农哈鲁，在LIG干了两年，做Web的时间不长。工作内容主要是用php写写后端，用JavaScript・CSS实现一些前端的炫酷动画效果。

在写前端时总会被CSS搞得晕头转向，忘记某段代码会产生怎样的效果，为此收藏了一些工具站点，忘记时翻出来看看。

今天就来介绍几个这样的工具站点。

## 检视transform(变换)效果

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/07/150147150587635600_46.png)

[CSS3 Generator](http://ds-overdesign.com/transform/matrix3d.html)

transform中的3D变换有时光靠想的话很难想明白，这个时候我会使用这个生成器来检视效果。

可以直接使用`rotate`与`translate`进行较为简单的动作，若动作较为复杂的话需要使用Matrix3D，设计具体的矩阵参数，在真正编码之前可以在这个网站上试试动作效果。

## 检视gradation(渐变)效果

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/07/15014715306973000_80.png)

[Ultimate CSS Gradient Generator](http://www.colorzilla.com/gradient-editor/)

有很多网站都应用了渐变色的设计，当使用多种颜色时可以像在Photoshop中那样设置，复制粘贴生成的代码即可产生同样的效果，对于用过Photoshop的人来说应该没什么问题=。

## 检视easing(缓动)效果

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/07/150147154625583000_96.png)

[Ceaser](https://matthewlein.com/ceaser/)

这是我最常使用的一个生成器。设置为默认的ease就可以得到一个很舒服的缓动效果，改变easing的选项可以选择其他不同的缓动风格。

使用这个生成器可以观察不同easing之间的微妙差别。我觉得通过改变属性值能即刻看到效果是很有趣的，自从知道了它，做图像缓动腰不酸了腿不痛了，一口气能做十张了。

## 番外篇

与生成器站点有所不同，使用[Adobe Assets](https://assets.adobe.com/)可以提高整体的工作效率。通过这个工具可以正确读取并展示设计师的设计图样。

使用Assets中的功能将Photoshop文件上传到AdobeCrowd上，不仅可以轻松的提取出字体大小、文本等，还可以获得特定的文本与图层的CSS。也可以一览所使用的色彩来确认图像的风格。

某些部分可能跟在Web页面上的表现有所不同，仅作为参考，不过用起来还是省了不少事。详细情况的话下次写一篇文章来介绍，给感兴趣的人一个参考。

## 总结

介绍的这些都是我经常使用的所见即所得的工具。

题外话，我觉得easing真是一种实现精细动作的高级工具啊。

都是些很常用的东西，如果没用过的话请务必试试~