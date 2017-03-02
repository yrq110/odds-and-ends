# 使用Web Audio Editor进行更直观的开发！Web Audio API入门（五）

***

>* 原文链接 : [使用Web Audio Editor进行更直观的开发！Web Audio API入门（五）
](https://liginc.co.jp/322853)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/01/148481536457291800_80-1310x874.jpg)

こんにちは。フロントエンドエンジニアのつっちーです。

タイトルの「続」に「々」が増えすぎてゾクゾクしていますが、引き続き「Web Audio API」入門です。

今回は、WebAudioAPIによる開発を補助してくれるFirefoxの機能、「Web Audio Editor」についてご紹介します。

## 「Web Audio Editor」とは？

Web Audio Editorは、Firefoxが提供する、WebAudioAPIを用いた開発のための補助機能です（2016年 11月時点で、他のブラウザでは同等の機能は提供されておりませんが、Web Audio APIが W3C の“勧告”となる頃にはきっと、他のブラウザにも高度な補助機能が備わっていることと思います）。

この機能は、AudioNode の接続状態を可視化し、AudioNode が持つ、各 AudioParamオブジェクトの valueプロパティを一覧表示します。

## 「Web Audio Editor」を使ってみよう
### 「Web Audio Editor」の起動

まず、Firefoxを起動しましょう。

Web Audio Editorは、Firefox の「開発ツール」の一部です。
そのため、Firefoxを起動したら、開発ツールを開きましょう。

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/01/148481503268393000_29.png)

Windowsでは、 ctrl + shift + I 、MacOSXでは command + option + I を押下することで開くことができます。

Web Audio Editorは、デフォルトでは無効化されています。開発ツールからオプションを選択し、「Web Audio」にチェックを入れましょう。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147822815299567000_66.png)

これでタブに「Web Audio」が追加され、Web Audio Editorが使用可能となります。

タブの「Web Audio」を選択した状態でページ遷移すると、遷移先のページで生成される AudioContext に対して検証が行われます。すでに表示しているページの AudioContext に対して検証を行う場合は、再読み込みを行ってください。


