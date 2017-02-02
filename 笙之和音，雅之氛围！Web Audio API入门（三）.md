# 笙之和音，雅之氛围！Web Audio API入门（三）

***

>* 原文链接 : [笙（しょう）の和音でみやびな気分！続々「Web Audio API」入門](https://liginc.co.jp/307261)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/09/147365738566254500_06-1310x874.jpg)


こんにちは。フロントエンドエンジニアのつっちーです。

前回、前々回では、音源として音声ファイルを扱いました。
次は音源もWebAudioAPIで生成してみましょう。

> ・この記事を読むときは、お使いのブラウザの他のタブ、ウインドウでWebAudioAPIが使用されていないことをご確認願います。
・コードプレビューのJS全体が即時関数で囲われている場合、その即時関数は実際には不要であると考えてください。
Webブラウザは同時に存在できるAudioContextオブジェクトの数に制限をかけています。
通常、AudioContextオブジェクトが1アプリケーションに複数必要となることはなく、この制限に困ることはありません。
ただし、複数のタブ、ウインドウ、iframeでWebAudioAPIが使用される場合にはエラー発生の可能性があるため、本記事では処理を即時終了させることで対策を行っております。

## ブラウザ上で音源を生成し再生するWebサイト

### Javascript Drone

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/07/waa011.png)

[http://matt-diamond.com/drone.html](http://matt-diamond.com/drone.html)

こちらは、以前にも紹介したドローンを再生するWebサイトです。

このドローンは複数の音源を同時発音することで表現されていて、その音源はWebAudioAPIを用いてブラウザ上で生成されています。
今回は、同じようにWebAudioAPIで音源を生成し、雅楽で用いられる管楽器、笙（しょう）（っぽいの）を作っていきます。
