# 学习SVG属性并制作动画
***

>* 原文链接 : [SVGのプロパティを理解してアニメーションさせてみよう](https://liginc.co.jp/312143)
* 原文作者 : [はやち](https://liginc.co.jp/member/member_detail?user=hayachi)
* 译者 : [yrq110](https://github.com/yrq110)

***

## SVG属性

下面介绍一下SVG的属性。

### fill

<p data-height="265" data-theme-id="0" data-slug-hash="xEgWpY" data-default-tab="css,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Fill" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/xEgWpY/">Fill</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

fill是设置元素内部填充的属性。

```css
fill:#fb9e28;
```

### fill-opacity

<p data-height="265" data-theme-id="0" data-slug-hash="GjAdKR" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Fill opacity" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/GjAdKR/">Fill opacity</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

fill-opacity是设置fill所填充区域透明度的属性。

```css
fill-opacity:0.3;
```

### stroke

<p data-height="265" data-theme-id="0" data-slug-hash="vXgjxY" data-default-tab="css,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/vXgjxY/">Stroke</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke是设置线条、文本和元素的轮廓线颜色的属性。

```css
stroke:#000;
```

### stroke-width

<p data-height="265" data-theme-id="0" data-slug-hash="qaRYmw" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke width" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/qaRYmw/">Stroke width</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-width是设置轮廓线宽度的属性。

可以使用的单位有px,em,ec,pt,pc,cm,mm,in。需要注意设置为0的话轮廓线会消失。( ˇωˇ)☝

```css
stroke-width:5px;
```

### stroke-opacity

<p data-height="265" data-theme-id="0" data-slug-hash="VKPxrw" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke opacity" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/VKPxrw/">Stroke opacity</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-opacity是设置stroke所描轮廓线透明度的属性。

```css
stroke-opacity:0.3;
```

### stroke-linecap

<p data-height="265" data-theme-id="0" data-slug-hash="zKNjZX" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke Linecap" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/zKNjZX/">Stroke Linecap</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-linecap是设置路径端点形状的属性。
```css
stroke-linecap:butt;

stroke-linecap:round;

stroke-linecap:square;
```
* butt
  与线平齐的形状
* round
  端点为圆形
* square
  端点为正方形
  
### stroke-linejoin

<p data-height="265" data-theme-id="0" data-slug-hash="ALOaVJ" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke linejoin" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/ALOaVJ/">Stroke linejoin</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-linejoin是设置路径间连接形状的属性。

```css
stroke-linejoin: miter;

stroke-linejoin: round;

stroke-linejoin: bevel;
```

* miter
  连接处为尖锐状
* round
  连接处为圆形
* bevel
  连接处为削平状

### stroke-dasharray

<p data-height="265" data-theme-id="0" data-slug-hash="qaRvVx" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke dasharray" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/qaRvVx/">Stroke dasharray</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-dasharray是设置线段间间隔的属性。

设为1px的话会使线段长度和线段间隔都为1px。

```css
stroke-dasharray: 1;
 
stroke-dasharray: 3;
 
stroke-dasharray: 10;
```

### stroke-dashoffset

<p data-height="265" data-theme-id="0" data-slug-hash="WGRmqx" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke dashoffset" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/WGRmqx/">Stroke dashoffset</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-dashoffset是设置线条起始位置的属性。

demo中所有线条的stroke-dasharray属性都是170px，可以看见移动位置后线条的长度发现了变化。

```css
stroke-dashoffset: 170;
 
stroke-dashoffset: 100;
 
stroke-dashoffset: 50;
```

有关stroke-dasharray与stroke-dashoffset属性的动画可以参考下这篇文章中的说明( ˘ω˘)☞三☞ｼｭｯｼｭｯ
[Animated line drawing in SVG](https://jakearchibald.com/2013/animated-line-drawing-svg/)

### 制作动画

<p data-height="265" data-theme-id="0" data-slug-hash="BLkZZd" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="SVG animation" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/BLkZZd/">SVG animation</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

※请点击RERUN播放动画

使用SVG属性来制作一些力所能及的动画( ˘ω˘)☞三☞ｼｭｯｼｭｯ

将圆形部分与面部元素部分分开制作。

首先设置stroke-dasharray使线间没有间隔。


```css
  fill:none;
  stroke:#000;
  stroke-width:4px;
  stroke-dasharray: 287;
}
 
path{
  fill:#000;
  fill-opacity:1;
  stroke:#000;
  stroke-width:1px;
  stroke-dasharray: 66;
}
```

使用animation属性设置动画( ˇωˇ)☝

圆形部分只设置stroke-dashoffset属性，面部元素部分一起设置stroke-dashoffset和fill-opacity属性( ˇωˇ)☝

```css
circle{
  animation: circle ease 3s;
}
path{
   animation: path ease 3s;
}
 
@keyframes circle {
  to {
    stroke-dashoffset: 0;
  }
  from {
    stroke-dashoffset: 287;
  }
}
 
@keyframes path {
  to {
    stroke-dashoffset: 0;
    fill-opacity:1;
  }
  from {
    stroke-dashoffset: 66;
    fill-opacity:0;
  }
}
```

### 总结

理解了这些属性后会对动画的属性设置有更深刻的理解吧( ˇωˇ )

那么回见₍₍ (ง ˘ω˘ )ว ⁾⁾
