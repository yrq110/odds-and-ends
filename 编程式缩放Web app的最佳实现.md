# 编程式缩放Web app的最佳实现

***

> * 原文链接 : [Best Way to Programmatically Zoom a Web Application](https://css-tricks.com/best-way-programmatically-zoom-web-application/)
> * 原文作者 : [MICHAEL ROMANOV ](https://css-tricks.com/author/romanovma-pookl/)
> * 译者 : [yrq110](https://github.com/yrq110)

***

网站的无障碍访问一直是很重要的，并且现在多数国家的政府都有了明确的标准与规范，因此使网站支持这些标准并增强可访问性变得很关键。

[W3C推荐标准](https://www.w3.org/TR/WCAG20/)中提供了一致性的三种等级：A, AA和AAA。为了达到AA这一级，除了满足其他要求外，我们还需要提供一种增加网站字体大小的方法：

> 1.4.4 Resize text: Except for captions and images of text, text can be resized without assistive technology up to 200 percent without loss of content or functionality. (Level AA)

让我们探索一些解决方案并找出一种最好的。

## 不完美的解决：CSS zoom

当提到尺寸变化时最先想到的就是缩放，CSS中的zoom属性所产生的效果正是我们想要的 - 增大尺寸。

先来看一个常用的设计方案(之后也会用这个例子)：一个水平导航栏，遇到断点时会变为一个菜单图标：

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_600,f_auto,q_auto/v1504271500/1-RNslcYJZjmPXgv4M_enFYw_bxwlwd.gif)

> 这是我们想要的效果，不会发生折叠，并且在特定的断点会变为一个菜单图标

下面的GIF展示了对菜单元素执行的zoom操作，我创建了一个开关来调整不同的尺寸与缩放级别：

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_600,f_auto,q_auto/v1504271653/1-y39NlrZDeYXR0KTPnSCL_Q_vr2m2w.gif)

> 想试玩的话可以看看这个[Pen](https://codepen.io/romanovma/pen/mMxEJN)

可以看到菜单超出了可视范围，这是由于使用zoom不能编程式的增加viewport的宽度，并且由于需求也不能进行折叠。菜单图标也没有出现，因为实际的屏幕尺寸没有变化，与点击开关前的尺寸相同。

不仅如此，Firefox目前还不支持zoom。

## 错误的解决：Scale transform

可以使用`transform: scale`进行缩放达到与`zoom`相同的效果，并且transform的兼容性更好，不过也会出现与`zoom`相同的问题：菜单没有出现在可视区域中，甚至更糟，菜单部分还超出了竖直方向的可视区域，这是由于页面布局的缩放系数是基于初始为1的scale计算的。

<p data-height="265" data-theme-id="0" data-slug-hash="VzXjQZ" data-default-tab="css,result" data-user="romanovma" data-embed-version="2" data-pen-title="Font-switcher--wrong-scale" class="codepen">See the Pen <a href="https://codepen.io/romanovma/pen/VzXjQZ/">Font-switcher--wrong-scale</a> by Mikhail Romanov (<a href="https://codepen.io/romanovma">@romanovma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 另一种不完美的解决：rem 与 html font-size

除了zoom与scale方法外，可以将rem作为页面中所有元素的长度单位，并通过改变html元素的font-size属性来改变它们的尺寸，因为1rem等于html的font-size值。

这是个相当不错的解决方案，不过并不完美。如下面的demo所见，有如前面的例子同样的问题：在断点时水平方向并未适配，因为所需空间增大了但viewport宽度并未改变。

<p data-height="265" data-theme-id="0" data-slug-hash="GvMZop" data-default-tab="css,result" data-user="romanovma" data-embed-version="2" data-pen-title="Font-switcher--wrong-rem" class="codepen">See the Pen <a href="https://codepen.io/romanovma/pen/GvMZop/">Font-switcher--wrong-rem</a> by Mikhail Romanov (<a href="https://codepen.io/romanovma">@romanovma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

从一定程度上来说，这个问题是由于媒体查询并不会根据尺寸的变化而调整。当我们增大尺寸时，媒体查询应该对应调整断点尺寸，这样在修改尺寸后相关的内容才会产生预期的效果。

## 可行的解决：使用Sass mixin模拟浏览器缩放

为了寻找灵感，来看看本地浏览器是如何处理缩放的：

![](https://res.cloudinary.com/css-tricks/image/upload/c_scale,w_600,f_auto,q_auto/v1504271851/browser-zoom_oo4vey.gif)

哎哟我去！聪明的Chrome理解了缩放会影响实际的viewport。放大会使viewport变窄，这样媒体查询会产生我们所期望的效果。

一种实现的方法(不依靠本地缩放，因为我们无法通过页内符合AA级的控件来访问这个功能)是每次改变font-size时都更新媒体查询中的值。

举个栗子，比如我们媒体查询的断点是1024px并且接下来要进行一个200%的缩放。为了适应新的尺寸需要将断点更新为2048px。

这不是很简单吗？难道我们不能使用rem来设置媒体查询的尺寸使得当我们增大font-size时媒体查询会自动调整？遗憾的是no，这并没效果，看看这个[例子](https://codepen.io/romanovma/pen/GvMZop)，会发现改成rem的话没有变化。在增大尺寸后布局并没有切换断点，这是因为根据[规范](https://www.w3.org/TR/css3-mediaqueries/#units)中，媒体查询中的rem与em单位是基于html元素初始的font-size值(默认为16px，可修改)计算的。

> Relative units in media queries are based on the initial value, which means that units are never based on results of declarations. For example, in HTML, the em unit is relative to the initial value of 'font-size.

即便如此我们可以使用Sass中的mixin(译者：less中的mixin亦可)来实现！下面是实现方法：

1. 在html元素上为每种尺寸新建一个特殊类（font-size--s, font-size -- m, font-size--l, font-size -- xl等）
2. 创建一个特殊的mixin，为每一种断点、尺寸与对应的内容创建媒体查询规则
3. 在所有想要执行媒体查询的地方使用这个mixin包裹代码

mixin长这样：
```scss
$desktop: 640px;
$m: 1.5;
$l: 2;
$xl: 4;
// 这里是关键，当增大font-size时需要增大min-width
@mixin media-desktop {
  html.font-size--s & {
    @media (min-width: $desktop) {
      @content;
    }
  }
  html.font-size--m & {
    @media (min-width: $desktop * $m) {
      @content;
    }
  }
  html.font-size--l & {
    @media (min-width: $desktop * $l) {
      @content;
    }
  }
  html.font-size--xl & {
    @media (min-width: $desktop * $xl) {
      @content;
    }
  }
}
.menu {
  @include media-desktop {
    &__mobile {
      display: none;
    }
  }
}
```
生成的CSS像下面这样：
```css
@media (min-width: 640px) {
  html.font-size--s .menu__mobile {
    display: none;
  }
}
@media (min-width: 960px) {
  html.font-size--m .menu__mobile {
    display: none;
  }
}
@media (min-width: 1280px) {
  html.font-size--l .menu__mobile {
    display: none;
  }
}
@media (min-width: 2560px) {
  html.font-size--xl .menu__mobile {
    display: none;
  }
}
```

若我们有n个断点和m种尺寸，需要生成n*m种媒体查询规则，这会包含所有情况，这样当字体大小增大时会使用新增的媒体查询规则。

看看下面这个Pen：

<p data-height="265" data-theme-id="0" data-slug-hash="JyrbOQ" data-default-tab="css,result" data-user="romanovma" data-embed-version="2" data-pen-title="Font-switcher--right" class="codepen">See the Pen <a href="https://codepen.io/romanovma/pen/JyrbOQ/">Font-switcher--right</a> by Mikhail Romanov (<a href="https://codepen.io/romanovma">@romanovma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 不足

这种方法有一些不足之处，来看看如何处理它们。

### 更多特定的媒体查询选择器

媒体查询中的所有代码都会因为在html.font-size — x选择器中而获得一定的特殊性。因此如果我们先用移动端访问的话，比如一个应用了无边距样式的元素会被桌面端的默认样式所覆盖，执行桌面端的外边距。

为了避免这个问题我们可以为移动端创建相同的mixin，不仅混入桌面端的代码也要混入移动端的CSS代码中，这样就平衡了特殊性。

其他方法可以通过手动增加针对每个特定情况的单独处理，或者创建具有期望功能的mixin(比如无外边距)然后将其混入每一个断点代码中。

### 更多生成的CSS

生成的CSS数量将会增加，毕竟我们针对每种尺寸都生成了CSS代码。

如果文件使用gzip压缩(通常也是这么做的)的话这并不是一个问题，因为它对重复代码处理的很好。

### 一些如Zurb的前段框架在JS util与CSS媒体查询中使用内置的断点

这个有点难办，就我个人而言会避免使用框架中依赖屏幕宽度的功能，最容易被忽略的就是网格系统，不过随着flex与grid布局的出现这也就不是个问题了，可以看看[这篇](https://zellwk.com/blog/responsive-grid-system/)文章，教你如何构建自己的网格系统.

不过如果一个项目依赖了这种框架或者我们不想去纠结这种特殊性问题，但还想实现AA级标准的话可以考虑使用rem单位而不是使用固定高度定义元素，通过调整html的font-size来更新布局与文本尺寸。
