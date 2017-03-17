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
