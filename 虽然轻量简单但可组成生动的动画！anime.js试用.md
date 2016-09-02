#虽然轻量简单但可组成生动的动画！anime.js试用
***

>* 原文链接 : [虽然轻量简单但可组成生动的动画！anime.js试用](http://liginc.co.jp/302886)
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

## 尝试anime.js

首先动起来，只写一个小球向上移动的动画可以吧！

<p data-height="265" data-theme-id="0" data-slug-hash="EyzomK" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/EyzomK/">anime.js Sample - Simple Animation</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

基本的使用方法: 首先指定target，然后指定想要变化的值与想要给予的动画属性，就可以了。关于这些属性，之后会逐一介绍。

### targets

在targets中设定执行动画的元素，可以通过以下方法指定。

| 种类	| 例子	|
| ----- | --- |
| CSS选择器	|	'.ball', '#container'	|
| DOM元素	|	document.querySelector('#container')	|
| Node列表	|	document.querySelectorAll('.ball')	|
| 数组	|	['.ball', '#container']	|

也可以在targets中输入对象，比如像这样伴随缓动的效果改变值的大小。

<p data-height="265" data-theme-id="0" data-slug-hash="qNQAgB" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/qNQAgB/">anime.js test - object properties</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

### 可以执行动画的参数

| 种类	| 例子	|
| ----- | --- |
| CSS属性	| width, backgroundColor, 'border-radius'等	|
| CSS 可以进行Transform操作的属性 | tranlateX, scale, rotate等	|
| SVG属性	| d, rx, transform等	|
| tag属性	| value, volume等	|
| 对象值	| 可以指定对象的key	|

可变化的值除了纯数字以外也可以输入带px、%、rem、vw等单位的值。

### 其他参数

为了对动画进行调整还准备了其他各种各样的属性。

| 名称	| 默认值	|   |
| ---- | ---- | ---- |
| delay	| 0	| 设定动画开始的毫秒数	|
| duration	| 0	| 设定动画持续的毫秒数	|
| autoplay	| true	| 设定执行时自动播放动画	|
| loop	| false	| 设定是否循环动画。	|
| direction	| 'normal'	| 设定动画的播放方向。可以'normal', 'reverse', 'alternate'中进行	|
| easing	| 'easeOutElastic'	| 设定缓动效果，可以通过console.log(anime.easings)来查看可使用的种类	|
| elasticity	| 400	| 调整动画的弹性大小	|

## 改变每项参数来调整动画

接着改变参数来调整动画。

给每个属性都设定一下目标值，可以设置duration、delay、easing等值。例子如下。

<p data-height="265" data-theme-id="0" data-slug-hash="QEJdrj" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/QEJdrj/">anime.js sample - Specific animation parameters</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

分别设定translateY与rotateY，小球上升后紧接着会翻转。

## 设定参数的起始值与终止值

通过数组输入起始值与终止值，0位是起始值，1位是终止值。

<p data-height="265" data-theme-id="0" data-slug-hash="KrAoAg" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/KrAoAg/">anime.js Sample - From To values</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

## 操作特定的元素值

有时在targets中会存在多个元素，可以使用函数来指定各元素的值。

第一个参数是被处理的target，第二个参数为target的索引值。函数的返回值即为target对应的属性值。

<p data-height="265" data-theme-id="0" data-slug-hash="jAQzjV" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/jAQzjV/">anime.js Sample 1 Specific target values</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

## 控制动画的播放与暂停

anime.js不仅可以进行动画的播放与暂停，也可以根据进度来表示动画。


| 名称	| 默认值 |
| ---- | ---------- |
| .play()	| 播放动画 |
| .pause()	| 暂停动画 |
| .restart()	| 重新播放动画 |
| .seek()	| 通过进度表示动画，在0~100之间取值 |

<p data-height="265" data-theme-id="0" data-slug-hash="rLQvaG" data-default-tab="css,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/rLQvaG/">anime.js Sample - Multiple timing values</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

## 路径动画

可以沿着SVG路径来执行动画。

使用anime.path()函数来得到动画执行的路径，将参数设为想得到的路径对象。

可以使用translateX、tranlateY、rotate 3种属性来改变通过anime.path()得到的路径对象。

<p data-height="265" data-theme-id="0" data-slug-hash="xOQjOQ" data-default-tab="html,result" data-user="Im0-3" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/Im0-3/pen/xOQjOQ/">anime.js Sample - Path Animation</a> by Yusuke Omi (<a href="http://codepen.io/Im0-3">@Im0-3</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

## 总结

感觉怎么样？操作简单，有丰富的淡入淡出等渐变效果，并且能调整附带的弹性效果，轻轻松松就能设计出生动的动画。

虽然有时使用复杂的动画效果更好，不过从使用简单动画实现开始也未尝不可，请务必把玩一下下！

PS: 顺便放上根据anime.js作者的例子自己弄的[demo](http://codepen.io/yrq110/pen/YGzZRE)
