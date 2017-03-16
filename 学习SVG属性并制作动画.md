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

fillは、要素の内部の塗りを指定できるプロパティです。

fill:#fb9e28;

### fill-opacity

<p data-height="265" data-theme-id="0" data-slug-hash="GjAdKR" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Fill opacity" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/GjAdKR/">Fill opacity</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

fill-opacityは、fillで塗られた箇所の透明度を変えることができるプロパティです。

fill-opacity:0.3;

### stroke

<p data-height="265" data-theme-id="0" data-slug-hash="vXgjxY" data-default-tab="css,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/vXgjxY/">Stroke</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

strokeは、線、テキスト、要素のアウトラインの色を指定できるプロパティです。

stroke:#000;

### stroke-width

<p data-height="265" data-theme-id="0" data-slug-hash="qaRYmw" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke width" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/qaRYmw/">Stroke width</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-widthは、外形線の幅を指定できるプロパティです。
px,em,ec,pt,pc,cm,mm,inでの単位で指定することができます。0を指定すると、ストロークの線が消えてしまうので注意です( ˇωˇ)☝

stroke-width:5px;

### stroke-opacity

<p data-height="265" data-theme-id="0" data-slug-hash="VKPxrw" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke opacity" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/VKPxrw/">Stroke opacity</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-opacityは、strokeで塗られた箇所の透明度を変えることができるプロパティです。

stroke-opacity:0.3;

### stroke-linecap

<p data-height="265" data-theme-id="0" data-slug-hash="zKNjZX" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke Linecap" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/zKNjZX/">Stroke Linecap</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-linecapは、パスの端に形状を指定するプロパティです。

stroke-linecap:butt;

stroke-linecap:round;

stroke-linecap:square;

* butt
  線に等しく平らな形状
* round
  線の端を丸くする
* square
  線の端を四角くする

### stroke-linejoin

<p data-height="265" data-theme-id="0" data-slug-hash="ALOaVJ" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="Stroke linejoin" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/ALOaVJ/">Stroke linejoin</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

stroke-linejoinは、パスのつなぎ目の形状を指定するプロパティです。

stroke-linejoin: miter;

stroke-linejoin: round;

stroke-linejoin: bevel;

* miter
  つなぎ目が鋭利な形状
* round
  つなぎ目が丸い形状
* bevel
  つなぎ目が平らな形状
