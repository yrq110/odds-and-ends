# CSS中使用SVG制作选择框组件
***

> * 原文链接 : [JavaScript不使用！ SVGを使ってCSSでチェックボックスを作る方法](https://liginc.co.jp/315466)
> * 原文作者 : [はやち](https://liginc.co.jp/member/member_detail?user=hayachi)
> * 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/12/14832784866283400_43-1310x874.jpg)


大家好₍₍ (ง ˘ω˘ )ว ⁾⁾

这次使用之前所说的SVG动画来进行选择框组件的制作( ˇωˇ)☝

之前的教程：[学习SVG属性并制作动画](https://github.com/yrq110/odds-and-ends/blob/master/%E5%AD%A6%E4%B9%A0SVG%E5%B1%9E%E6%80%A7%E5%B9%B6%E5%88%B6%E4%BD%9C%E5%8A%A8%E7%94%BB.md)

## 实现

首先介绍实现的方法( ˇωˇ)☝

### 标签

把SVG标签放入label内( ˇωˇ)☝

```html
<ul>
    <li>
        <input type="checkbox" id="check-00" />
        <label for="check-00">Drawing a check box
            <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px"
                 y="0px" viewBox="0 0 32 32" style="enable-background:new 0 0 32 32;" xml:space="preserve">
            <path class="st0" d="M6,10.5c-0.2,1.7-0.4,5.2-0.7,6.6c-0.8,2.7-1.7,5.3-2.7,7.8c3.5-2,8.9-7.5,13.3-11.3c1.2-1,2.5-2.1,3.9-2.8
                    c3-1.4,6.2-2.6,9.7-0.8"/>
            </svg>
        </label>
    </li>
</ul>
```

### 样式
#### 设置SVG与动画

设置SVG的初始属性与动画。

由于是描边动画，需要设置stroke-dasharray填充所有的线条间距，并将stroke-offset设为同样的值( ˇωˇ)☝

这次把动画的stroke-offset（线条位置）与 stroke-opacity（线条透明度）属性的变换时间改为0.3s( ˇωˇ)☝

```scss
ul li{
  list-style: none;
  color: #000;
  font-size:25px;
  position: relative;
  margin-bottom: 25px;
}
 
svg{
  width: 24px;
  height: 24px;
  left : 7px;
  top : 4px;
  position: absolute;
  z-index: 1;
 
  path{
    fill: none; //无填充色
    stroke: #000; //设置线条颜色
    stroke-linejoin:round; //路径连接点为
    stroke-linecap:round; //路径线帽为圆角
    stroke-dasharray: 51; //设置线条间隔
    stroke-dashoffset:51; //设置线条长度
    stroke-opacity:0; //设置线条透明度
    stroke-width:4px; //设置线条宽度
    transition: stroke-dashoffset 0.3s ease, stroke-opacity 0.3s;
    //▲线条长度与透明度的动画
  }
}
```
#### 设置选择框

当选择框被选中时增加checked伪元素效果，执行动画，并且同时间接的选中了label、svg、path元素。

在选中checked状态时，会执行stroke-dashoffset 与 stroke-opacity 动画( ˇωˇ)☝

```scss
input[type=&quot;checkbox&quot;]{
  -webkit-appearance: none;
  display: inline-block;
  width: 35px;
  height: 35px;
  background: #fff;
  vertical-align: top;
  position: relative;
  top: -5px;
  margin-right: 10px;
  box-sizing: border-box;
  border: 3px solid #999;
  border-radius: 3px;
  transition: border 0.3s;
 
  &:focus{
    outline:rgba(0,0,0,0);
  }
  &:checked{
    border: 3px solid #000;
  }
  &:checked ~ label{
    color: #000;
  }
  &:checked ~ label:before{
    border: 3px solid #000;
  }
  &:checked ~ label svg path{
    stroke-dashoffset:0;
    stroke-opacity:1;
  }
}
 
label{
  cursor: pointer;
  color: #999;
  transition: color　0.3s；
}
 
label:before{
  content : '';
  display: inline-block;
  width: 28px;
  height: 28px;
  margin-right: 15px;
  position: relative;
  top: 7px;
  border: 3px solid #999;
  border-radius: 3px;
}
```

实际效果如下所示( ˘ω˘)☞三☞ｼｭｯｼｭｯ

<p data-height="265" data-theme-id="0" data-slug-hash="ZBYqyW" data-default-tab="css,result" data-user="Hayachi" data-embed-version="2" data-pen-title="SVG CheckBox" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/ZBYqyW/">SVG CheckBox</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 试试其他样式
理解实现的原理后，就可以通过改变SVG来实现不同的选中效果了( ˇωˇ)☝

### 填充型选择框
实现涂鸦时沙沙作响的填充效果( ˇωˇ)☝

<p data-height="265" data-theme-id="0" data-slug-hash="LbVLYr" data-default-tab="html,result" data-user="Hayachi" data-embed-version="2" data-pen-title="SVG CheckBox" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/LbVLYr/">SVG CheckBox</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

### 双线选择框
设置SVG中两个path元素不同的delay值，使其按顺序进行绘制( ˇωˇ)☝

<p data-height="265" data-theme-id="0" data-slug-hash="rWVzjP" data-default-tab="css,result" data-user="Hayachi" data-embed-version="2" data-pen-title="SVG CheckBox" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/rWVzjP/">SVG CheckBox</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 总结

我觉得只用CSS来实现选择框样式的方法是很简单的。

悄无声息的进行了动画的演出，有点小激动哦₍₍ (ง ˘ω˘ )ว ⁾⁾

之后也可以使用这种方法实现其他样式哦( ˇωˇ)☝

那么回见~((((´ʘ‿ʘ｀)
