# 初次使用phina.js - JavaScript游戏开发库
***

>* 原文链接 : [はじめてのphina.js – JavaScriptゲームライブラリを使ってみた！](https://liginc.co.jp/306739)
* 原文作者 : [シスコ](https://liginc.co.jp/member/member_detail?user=cisco)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147263633475346200_15-1310x874.jpg)

大家好！这次来一起体验下phina.js！在下面的内容中我会介绍它的导入方法与基础操作。

# phina.js是什么？

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147205642564284300_35.png)

phina.js是用JavaScript编写的一种制作游戏与工具的库，可以用来制作PC端与移动端的小游戏。

不过，由于是国产的(PS：指日本)，参考文档是日语，可能对初学者来说不太友好。

# 使用前的准备工作

在任一html文件的head标签内添加如下代码:

```html
<script src="phina.min.js"></script>
```

接着创建执行phina.js的js文件，添加如下代码:

```javascript
// app.js
 
// phina.js をグローバルに展開
phina.globalize();
 
// 定义MainScene
phina.define('MainScene', {
    superClass: 'CanvasScene',
    init: function() {
        this.superInit();
        this.backgroundColor = '#185674'; // 任意背景色
    }
});
 
// 主函数
phina.main(function() {
    // 创建应用
    var app = GameApp({
        startLabel: 'main'
    });
 
    app.run();
});
```

搞定以后在本地浏览器中运行一下试试。

在上面代码中设置了背景色，若出现有颜色的Canvas的话就表示成功了！

# 开始使用phina.js

完成准备工作后，是时候介绍phina.js的基础部分了！

## 标签-Label

在表示游戏开始、游戏结束与重新开始等画面上的文本时一般都会用到标签。

```javascript
var label = Label('文本内容').addChildTo(父元素);
```

像上面那样编写就可以用标签表示文本内容了。

如下在刚才创建的js文件的MainScene函数中部分代码:

```javascript
// 省略
--------------------------------------
 
    // 定义MainScene
    phina.define('MainScene', {
        superClass: 'CanvasScene',
        init: function() {
            this.superInit();
            this.backgroundColor = '#185674'; // 任意背景色
 
            var x_grid = this.gridX;　// x坐标
            var y_grid = this.gridY;　// y坐标
 
        // 创建标签
        var label = Label({
            text: 'Hello!!, Get strat phina.js!',
            fill: 'white',
            fontSize: 40
        }).addChildTo(this);
        label.setPosition(x_grid.center(),y_grid.center());　// 居中
            }
        });
 
    // 主函数
    phina.main(function() {
 
    --------------------------------------
    // 省略
```

如果在之前的Canvas中出现了指定的文本内容就成功了！

Label类可以指定标签的填充类型、字体大小与边框类型。

## 图形的绘制与图像的表示

可以绘制多种默认图形，图像的表示也很简单。

### 图形的绘制

用于绘制图形的代码:

```javascript
var shape = 默认的图形类(options).addChildTo(父元素);
```

可以使用下面这些图形类：

* CircleShape: 圆
* RectangleShape: 矩形
* TriangleShape: 三角形
* StarShape: 星形
* PolygonShape: 多边形
* HeartShape: 心形

来试试赋予不同的option，看看有什么效果！

绘制图形与刚才的标签部分一样，也在Mainscene函数中编写。

```javascript
// 绘制图形
   var circle = CircleShape({
        fill: 'yellow',
        radius: 50
   }).addChildTo(this);
   circle.setPosition(x_grid.center(-4), y_grid.center(-2));
 
 
    var rect = RectangleShape({
        fill: 'green',
        stroke: '#fff',
        width: 100,
        height: 100
    }).addChildTo(this);
    rect.setPosition(x_grid.center(), y_grid.center(-2));
 
    var triangle = TriangleShape({
        backgroundColor: 'gray',
        fill: 'red',
        width: 80,
        height: 80
    }).addChildTo(this);
    triangle.setPosition(x_grid.center(4), y_grid.center(-2));
 
    var star = StarShape({
        stroke: 'gold',
        sideIndent: 0.7
    }).addChildTo(this);
    star.setPosition(x_grid.center(-4), y_grid.center(2));
 
    var polygon = PolygonShape({
        fill: '#66ffcc',
        sides: 5
    }).addChildTo(this);
    polygon.setPosition(x_grid.center(), y_grid.center(2));
 
    var heart = HeartShape({
        fill: '#ff82b2',
        cornerAngle: 30
    }).addChildTo(this);
    heart.setPosition(x_grid.center(4), y_grid.center(2));
```

执行后如下图所示：

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147205127294916200_83.png)

### 图像的表示

表示图像的方法如下。

首先，可以在创建GameApp类的同时导入图像与音乐等资源。

```javascript
var app = GameApp({
    startLabel: 'main',
    assets: img　//asset名随意
});
```

使用[key: 读取资源的路径]的格式来指定想要表示的图像

```javascript
// 示例
var img = {
    image: {'key': '读取资源的路径'}
};
```

接着，在Mainscene中添加如下代码

```javascript
var usagi = Sprite('usagi').addChildTo(this);　// ('usagi')内填写指定的key
usagi.setPosition(x_grid.center(), y_grid.center());
usagi.width = 240;
usagi.height = 240;
```

像这样写的话就能表示出想要读取的图像了！

### 没事儿走两步！

接下来介绍如何赋予元素移动与旋转的动作。

#### 元素移动

给想要移动的元素的update变量赋予一个函数就可以让它进行简单的移动了！

我打算让之前表示的图像上下移动！（移动与图形的形状无关）

```javascript
// 图像表示
        var usagi = Sprite('usagi').addChildTo(this);
        usagi.setPosition(x_grid.center(), y_grid.center());
        usagi.width = 150;
        usagi.height = 150;
 
        // 移动速度
        usagi.speed = 15;
 
        // 动作处理
        usagi.update = function() {
            this.y += this.speed;
 
            // 限定移动范围
            if(this.top <= 300) {
                this.top = 300;
                this.speed *= -1;
            } else if(this.bottom >= 550) {
                this.bottom = 550;
                this.speed *= -1;
            }
        }
```
usagi.update変数の記述以下が追加したコードになります。

实际在浏览器中的效果如下所示：

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147205994890869900_78.gif)

使用rotation属性加上旋转的动作。

怎么感觉有点蛋疼…！（:-D）

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147206113880380600_51.gif)

### 添加事件！

这次介绍触摸类事件。

```javascript
el.setInteractive(true);
```
このように指定することで、タッチ系のイベントを有効にすることができます。

下に書いてあるようなイベントを登録することができます！
```javascript
// 触摸开始时
el.onpointstart = function() {
}
 
// 触摸移动中
el.onpointmove = function() {
}
 
// 触摸结束时
el.onpointend = function() { 
}
 
// 複数登録も可能
el.on('pointstart', function() { 
});
```
タッチイベントを適用させたデモです！

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147207384628147100_30.gif)

画像のランダム表示は結構難しかったです。。。

### 当たり判定をしてみる！

ゲームといえば当たり判定はつきものですね！
難しいと思うことなく、比較的簡単に当たり判定を実装できちゃいます！

`hitTestElement()`を使うことによって、他要素との当たり判定を行えるようになります。
```javascript
// あたり判定コード 例
var a;
var b;
 
if(a.hitTestElement(b)) {
  // 当たったときの処理
}
```
当たり判定のデモです。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147207737883824200_73.gif)

### TweenAnimationをつけてみる！

tweenerというプロパティを使用することで要素にアニメーションを付け加えることができます。
面白いところだと思うので、一緒にやってみましょう！

Tweenアニメーションは下記のコードで適用されます！

```javascript
el.to({y: 200}, 5000, 'easeOutElastic') // y軸を5秒かけて200に変化
```

先ほどの当たり判定のデモを編集してジャンプモーションとBoxに当たったときのTweenerアニメーションを追加してみました！

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147208215927923500_85.gif)

# まとめ

phina.jsいかがでしたか？
そこまで複雑なコードを書かなくても、簡単にアニメーションや動きをつけられるのはすごいですよね！！
少しでも面白そうだなって思った人は、ぜひ使ってみてください！　やってて楽しいですよ！
今回は基本編でしたが、もうちょっと応用の部分も紹介できたらと思います。
それでは、これにてっ！
