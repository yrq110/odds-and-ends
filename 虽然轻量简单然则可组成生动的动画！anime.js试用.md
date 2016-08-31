#虽然轻量简单然则可组成生动的动画！anime.js试用
***

>* 原文链接 : [虽然轻量简单然则可组成生动的动画！anime.js试用](http://liginc.co.jp/302886)
* 原文作者 : [店長](http://liginc.co.jp/author/omi)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](http://cdn.liginc.co.jp/wp-content/uploads/2016/08/147185186778975000_08.png)

大家好，请问大家都是怎样实现动画的呢？

这次来介绍一下anime.js动画库的简单使用。

anime.js中可以操作的有:CSS、标签属性、SVG、对象值，并且非常轻量！

这是与其它动画库文件大小的比较。

| 库 | 大小 |
| ---------  | ---- |
| Tween.js v.0.6.2 | 103 KB |
| TweenMax v.1.19.0	| 347 KB	|
| TweenLite v.1.19.0	| 31.9 KB	|
| anime.js v1.1.0	| 19.9 KB	|
| anime.js v1.1.0（minify）	| 9.21 KB	|

与[Tween.js](http://www.createjs.com/tweenjs)和[之前づや桑介绍的TweenMax](http://liginc.co.jp/web/js/other-js/94188)相比要小很多。

当然，与其它库相比的话功能有限，即便如此也可以使用简单的动画来实现丰富的表现。实际上我也做出了这样的demo。

Demo:
<p data-height="265" data-theme-id="0" data-slug-hash="BzGxWL" data-default-tab="js,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/BzGxWL/">anime.js Sample - demo</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

使用方法非常简单，记住后就可以做出简单的动画了！库支持以下浏览器。

* Chrome
* Safari
* Opera
* Firefox
* IE 10+

IE对应10以上的版本。那么赶快来看看使用方法吧。

## 尝试anima.js

首先动起来，只写一个小球向上移动的动画可以吧！

<p data-height="265" data-theme-id="0" data-slug-hash="EyzomK" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/EyzomK/">anime.js Sample - Simple Animation</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

基本的使用方法: 首先指定target，然后指定想要变化的值与想要给予的动画属性，就可以了。关于这些属性，之后会逐一介绍。
