# 初次使用phina.js - JavaScript游戏开发库
***

>* 原文链接 : [はじめてのphina.js – JavaScriptゲームライブラリを使ってみた！](https://liginc.co.jp/306739)
* 原文作者 : [シスコ](https://liginc.co.jp/member/member_detail?user=cisco)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147263633475346200_15-1310x874.jpg)

こんにちは！　Nike大好き！ダンサー兼フロントエンドエンジニアのシスコです。
我が足は常にNikeと共にあり！というくらい毎日大切に履かせてもらってます。ダンスシューズもNikeに変えたら前より調子よいのです……。

それはさておき、今回はJavaScriptゲームライブラリであるphina.jsというのを一緒に触っていきましょう！！導入方法や基本的な操作の部分を説明できればと思います！

# phina.jsとは？

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/08/147205642564284300_35.png)

ゲームやツールなどを作れるJavaScript製のゲームライブラリです。PC, スマホ両方に対応しており、簡単にゲームが作れるみたいです！
また、国産なので日本語のリファレンスがあるというのも、これから初める人には優しくなっているところかもしれませんね。

# 使うための下準備

任意のhtmlファイルのhead内に下記のコードを追記してください。

```html
<script src="phina.min.js"></script>
```

続いてphina.jsで実行するjsファイルを作成し、下記のコードを追加しましょう！

```javascript
// app.js
 
// phina.js をグローバルに展開
phina.globalize();
 
// MainScene を定義
phina.define('MainScene', {
    superClass: 'CanvasScene',
    init: function() {
        this.superInit();
        this.backgroundColor = '#185674'; // 任意の背景色
    }
});
 
// メインの処理
phina.main(function() {
    // アプリケーションを生成
    var app = GameApp({
        startLabel: 'main'
    });
 
    app.run();
});
```

これが終わったら、一度お手元のブラウザで動いているかどうか確認してみましょう！
背景色として設定した、色のCanvasが表示されていれば成功です！
