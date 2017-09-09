#5分钟了解Material Design
***

> * 原文链接 : [今さら聞けない?! 5分でわかる！マテリアルデザイン入門](https://lab.sonicmoov.com/design/material-design/)
> * 原文作者 : ユウコ
> * 译者 : [yrq110](https://github.com/yrq110)

***

[Google Material Design指南](http://www.google.com/design/spec/material-design/introduction.html)。

距离2014年6月发布以来已经过了1年(ps:文章是2015年写的)，出现了不少符合Material Design风格的优秀UI/UX作品,Android自不必说，iOS的应用也不少。

为了让至今依旧流行的Material Design指南更通俗易懂，抓住要点讲解一下。

**目录**
* [何谓Material Design](#what-is)
  * [看似平面实则3D](#3d)
  * [纸与墨水](#paper)
* [Material Design的色彩](#color)
* [网格系统](#网格系统)
* [动画](#动画)
  * [舒服的变换](#舒服的变换)
  * [接触反馈](#接触反馈)
  * [有意义的动画](#有意义的动画)
* [总结](#总结)


<a name="what-is">
## 何谓Material Design？

Material Design直译过来就是[质感设计]。

数字设计中的[质感]体现在哪儿呢？来看两个概念。

<a name="3d"></a>
### 看似平面实则3D
Material Design通过物理手段来检测元素的重叠，在平面中具有明确的Z轴概念。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_3.png)

在表现元素的重叠与层次上阴影的效果功不可没。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_4.png)

与现实中的影子同理，阴影的表现会根据Z轴上的位置发生变化。

<a name="paper"></a>
### 纸与墨水
Material Design将导航栏、卡片列表、按钮等基本控件描述为[纸]，就是类似[纸]的东西。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_1.png)

这个[纸]会像现实中的纸一样重叠，由于是虚拟的可以随意的变大变小。

不过，像下图这样穿过一张纸等违反Material Design概念的行为是无效的。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_2.png)

还有，在纸上的文件与图标、图片等就像[墨水]一样。

文字和图片能理解成墨水，不过动画…？

虽说有违和感，不过Material Design是可以将动画当做墨水的。

由于这个[墨水]也是虚拟的，色彩与大小可以进行自由变换。

<a name="color"></a>
## Material Design的色彩
Material Design不能在同一个视图内使用过多的颜色。

视图中的基本元素由下面四种色彩构成。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_5.png)

* colorPrimary（主色）
* colorPrimaryDark (与colorPrimary是同系色)
* colorAccent (与colorPrimary相比较醒目的颜色，重点色)
* windowBackground (白色或透明的黑色，与colorPrimary是同系色)

Material Design Guideline中准备了调色板，不使用那些颜色就不能进行Material Design！才怪。

在重新设计现有元素时，最好将colorPrimary作为logo的主色调。

＜参考：[Material Design调色板](http://www.google.com/design/spec/style/color.html#color-color-palette)＞

## 网格系统
Material Design设计使用8dp的网格系统。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_6.png)

文本是4dp的网格。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_7.png)

上面的指南中提供了针对每一种UI组件的设计模板。

＜参考：[Material Design模板](http://www.google.com/design/spec/resources/layout-templates.html)＞

## 动画

对用户体验有很大影响的动画在Material Design中也是非常重要的。

关于动画有以下3个要点。

### 舒服的变换
动画执行时被赋予了物理的加减速效果，使这个过程更加自然，舒适。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_8.png)

### 接触反馈
在可以点击的场合下，必须做出一定的反馈表现。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_9.png)

### 有意义的动画
用户进行的按下按钮等操作与随后出现的动画，前后必须有紧密的关联性。

![](https://lab.sonicmoov.com/files/2015/07/materialdesign_10.png)

## 总结

Material Design对于设计师、工程师与用户来说都很容易理解，不过到了实际做应用或服务时，要完全按照指南中的规则做・・・并不是那么容易。

最重要的是需要考虑现在所做的应用与服务本身的理念与是否能为用户带来新的价值。

为了做出满足App理念与为用户带来价值的UI/UX设计，应该要充分掌握Material Design指南中的要素吧。
