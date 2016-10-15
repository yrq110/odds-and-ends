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

大多数情况下使用Illustrator导出SVG格式，你了解实际的DOM组成吗 SVG形式で書き出して使用するケースが多いですが、実際どういうDOM構造をしているのでしょうか。

来学习一下其中的构成，从绘制简单的图形绘制开始吧。

## SVGタグに必要な属性を記述しよう

首先需要SVG标签，如下所示：

```html
<svg xmlns="http://www.w3.org/2000/svg" width="600" height="600" viewBox="0 0 600 600">
```

xmlns属性的值为http://www.w3.org/2000/svg，表示svg的命名空间，吓着设置了所绘制区域的大小：width属性与height属性。 属性の値をhttp://www.w3.org/2000/svgとし、SVGであることを示します。次にwidth属性、height属性に、描画する領域の大きさを指定します。

viewBoxは表示領域の中の座標軸の設定です。左上の座標を(0,0)とし、そこから横に600、縦に600いったところに右下の座標を置きます。基本的に右下の座標はwidthとheightの値を入れておけばOKです。

## 線を描いてみよう

<p data-height="265" data-theme-id="0" data-slug-hash="rLkYxm" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/rLkYxm/">SVG line</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

線を描画するには、lineタグを使用します。x1,y1が起点の座標、x2,y2が終点の座標です。また、stroke-widthで線の太さ、strokeで線の色を指定できます。

## 丸を描いてみよう

<p data-height="265" data-theme-id="0" data-slug-hash="Krxyra" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/Krxyra/">SVG circle</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

円を描画するにはcircleタグを使用します。

cx,cyが円の中心点のx座標、y座標、rは円の半径です。fillにカラーコードやnoneを記述することで、円の中の塗りを指定することができます。

## 四角を描いてみよう

<p data-height="265" data-theme-id="0" data-slug-hash="dXqkrw" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/dXqkrw/">SVG  square</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

四角を描画するにはrectタグを使用します。

x、yには起点の座標、width、heightには起点からの距離を指定します。rx、ryは、角丸にしたい際に指定します。

## 三角を描いてみよう

<p data-height="265" data-theme-id="0" data-slug-hash="bZxYwE" data-default-tab="html,result" data-user="hatsushi_kazuya" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/hatsushi_kazuya/pen/bZxYwE/">SVG trigone</a> by k_hatsushi (<a href="http://codepen.io/hatsushi_kazuya">@hatsushi_kazuya</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

折れ線を描くにはpolylineタグ、多角形を描くにはpolygonを使用します。

書き始めたい座標をカンマ区切りで順に記述していきます。

上向き三角のコードで説明すると、

x座標200 y座標300

x座標350 y座標100

x座標500 y座標300

の位置に置いたパスを、順に結んでいます。

polylineタグとpolygonタグの違いは、パスを閉じるかどうかの違いしかありません。よって、上向き三角と下向き三角の間の線は、polygonタグで描いた下向き三角のものです。

# まとめ

今回は、図形を簡単に描ける方法をご紹介させていただきました。

位置を座標指定するのと、それぞれの形に応じたタグを使用することを覚えれば基本的な図形は難しくありません。

色を変えたり、形を組み合わせてたりして、動かしたりして、ぜひ表現の幅を広げてみてください！
