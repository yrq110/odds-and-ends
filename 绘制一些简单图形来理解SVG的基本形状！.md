# 绘制一些简单图形来理解SVG的基本形状！
***

>* 原文链接 : [簡単な図形を描きながら、SVGの基本的な仕組みを理解してみよう！](https://liginc.co.jp/300610)
* 原文作者 : [はっちゃん](https://liginc.co.jp/member/member_detail?user=kazuya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/09/147462935997857200_26-1310x874.png)

大家用SVG吗？

最近，由于log与图标在一些动态的表现效果中，扩大与缩小时画质会变差，为了避免这个问题而使用SVG的情况挺多的。

这次打算让大家通过绘制简单的图形来了解SVG的基本构成。

# SVG是什么

## 看起来跟图像一样

使用SVG绘制的数据一般作为SVG格式的图像。

## 可以做成动画

SVG标签与普通的HTML标签一样由DOM对象管理，使用javascripta来操作可以做成动画。

## 无负载的绘制

可以不用像图像那样作为文件存放在服务器上，而是无负载的在客户端一侧来动态生成画像。

## 支持的浏览器

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/ce5791a4c7b3c5cf05340237cbf64ebd.png)

支持除了IE8与Android2代以下之外的全部浏览器，支持的还是挺多的。

# 试着绘制SVG

大多数情况下使用Illustrator导出SVG格式，你了解实际的DOM组成吗。

来学习一下其中的构成，从绘制简单的图形绘制开始吧。

## 常用SVG标签与属性

首先需要SVG标签，如下所示：

```html
<svg xmlns="http://www.w3.org/2000/svg" width="600" height="600" viewBox="0 0 600 600">
```

xmlns属性的值为http://www.w3.org/2000/svg ，为svg的命名空间，接着使用width属性与height属性设置所绘制区域的大小。

viewBox设置所表示的区域，左上角的坐标为(0,0)，右下角的坐标为横向移动600，纵向移动600的位置，一般把width与height值代入右下坐标即可。

## 画线

<p data-height="265" data-theme-id="0" data-slug-hash="rLkYxm" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/rLkYxm/">SVG line</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

使用line标签来画线。x1,y1是起点坐标，x2,y2是终点坐标，另外，用stroke-width设置线条宽度，stroke设置线条填充颜色。

## 画圆

<p data-height="265" data-theme-id="0" data-slug-hash="Krxyra" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/Krxyra/">SVG circle</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

使用circle标签来画线。

cx,cy为圆心的x坐标与y坐标，r是圆的半径。赋予fill属性颜色码或none来设置内部填充的颜色。

## 画矩形

<p data-height="265" data-theme-id="0" data-slug-hash="dXqkrw" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/dXqkrw/">SVG  square</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

使用rect标签绘制矩形。

x、y为起点坐标，width与height为从起点开始的距离，可以使用rx、ry设置圆角。

## 画三角形

<p data-height="265" data-theme-id="0" data-slug-hash="bZxYwE" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/bZxYwE/">SVG trigone</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

使用polyline标签绘制折线，polygon标签绘制多边形。

按顺序编写坐标，使用逗号来分隔。

上面的三角形是按下面这些坐标

x坐标200 y坐标300

x坐标350 y坐标100

x坐标500 y坐标300

的顺序连接的路径。

polyline标签与polygon标签的区别是，在路径是否闭合这个问题上有所不同，因此，上三角与下三角中间的那条线是属于polygon标签所画的下三角。

# 总结

这一次介绍了简单图形的绘制方法。

若记住这些位置坐标的设置方法与各种图形标签的话，绘制基本图形就不是很难了。

请务必尝试一下诸如改变颜色、组合图形、动画等其它丰富的表现！
