# 画随音动！Web Audio API入门（四）

***

>* 原文链接 : [音にあわせて画面が変化！続々々「WebAudioAPI」入門](https://liginc.co.jp/310761)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

今回は、音源の解析と、その結果の視覚化について紹介します。

> ・この記事を読むときは、お使いのブラウザの他のタブ、ウインドウでWebAudioAPIが使用されていないことをご確認願います。
・コードプレビューのJS全体が即時関数で囲われている場合、その即時関数は実際には不要であると考えてください。
> Webブラウザは同時に存在できるAudioContextオブジェクトの数に制限をかけています。
通常、AudioContextオブジェクトが1アプリケーションに複数必要となることはなく、この制限に困ることはありません。
ただし、複数のタブ、ウインドウ、iframeでWebAudioAPIが使用される場合にはエラー発生の可能性があるため、本記事では処理を即時終了させることで対策を行っております。

## 音源の情報を解析し視覚化するWebサイト
### Loop Waveform Visualizer

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/06/waa03.png)

[https://airtightinteractive.com/demos/js/reactive](https://airtightinteractive.com/demos/js/reactive)
こちらは、以前にも紹介した音源を再生しながら視覚化するWebサイトです。

mp3ファイルを画面にドロップ、もしくは「load sample mp3」をクリックすると再生が始まります。

このサイトでは、瞬間瞬間の音量をWebAudioAPIによって解析し、音量の値が反映された円形をThree.jsによって描画することで、視覚化を実現しています。
音声ファイルの扱いに関してはこれまでの記事でも紹介してきましたので、この記事では、解析対象をマイクからの音声に置き換えてみましょう。

## 「Web Audio API」を使って音にあわせて画面を変化させてみよう

### マイクから取得した音を音源として利用してみる

音声や動画などのメディアコンテンツは、MediaStreamオブジェクトとして表現されます。MediaStreamオブジェクトは、navigator.mediaDevicesオブジェクトのメソッド、getUserMediaによって取得します。

このMediaStreamオブジェクトをWebAudioAPIから扱うには、MediaStreamAudioSourceNodeというAudioNodeを使用します。


