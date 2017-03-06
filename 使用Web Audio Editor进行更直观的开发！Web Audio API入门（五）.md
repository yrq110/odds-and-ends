# 使用Web Audio Editor进行更直观的开发！Web Audio API入门（五）

***

>* 原文链接 : [「Web Audio Editor」でより直感的なWeb Audio API開発を！ – 続々々々「Web Audio API」入門 ](https://liginc.co.jp/322853)
* 原文作者 : [つっちー](http://liginc.co.jp/member/member_detail?user=tsuchiya)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/01/148481536457291800_80-1310x874.jpg)

不知不觉已经到（五）了。

这次介绍一下Firefox中用于WebAudioAPI辅助开发的工具-「Web Audio Editor」。

## 「Web Audio Editor」是什么？

Web Audio Editor是Firebox浏览器所提供的一个WebAudioAPI辅助开发的工具(至2016年11月时还没有其他浏览器提供类似的功能，我觉得当Web Audio API成为W3C的推荐标准时，其他浏览器应该也会具备这个功能吧)。

使用这个工具可以看到AudioNode的连接状态、拥有的AudioNode与各AudioParam对象的value属性。

## 使用「Web Audio Editor」
### 打开「Web Audio Editor」

首先打开Firefox。

Web Audio Editor是Firefox浏览器开发工具中的一部分。因此打开Firefox后先打开开发工具。

![](https://cdn.liginc.co.jp/wp-content/uploads/2017/01/148481503268393000_29.png)

Windows下使用ctrl + shift + I快捷键，MacOSX下使用command + option + I快捷键。

由于默认是禁用Web Audio Editor的，需要在开发工具的设置里勾选上「Web Audio」（译者注:中文版的火狐浏览器中这个选项为「网络音频」）。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147822815299567000_66.png)

这样在标签栏中就有「Web Audio」了，可以正常使用Web Audio Editor了。

选中标签栏中「Web Audio」会有一个过渡页面，会对过渡前页面的AudioContext进行验证。若已经对当前页的AudioContext进行验证过了，就不用再次载入了。

### 检查AudioNode的连接状态

在使用Web Audio API开发时，会使用AudioNode的connect方法将多个AudioNode连接起来。在操作大量AudioNode的场合下，有时需要根据条件切换AudioNode间的连接状态，这时就很难通过代码来掌握AudioNode之间的连接状态吧。

Web Audio Editor通过将AudioNode的连接状态可视化来解决这个问题。

来实际操作下Web Audio Editor检查连接状态吧。

首先看看将表示音源的AudioNode连接到表示最终输出的AudioNode上的[demo](https://lig-dsktschy.github.io/wpapi-osc/1/)(点击链接前注意播放音量)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823213859569600_70.png)

每个AudioNode都用一个框表示，并使用一个箭头连接线表示执行connect方法的AudioNode与目标AudioNode之间的连接。

下面来看看同时输出多个音源的[demo](https://lig-dsktschy.github.io/wpapi-osc/2/)(点击链接前注意播放音量)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823215716495900_11.png)

所有表示音源的AudioNode都连接到了表示最终输出的AudioNode上，使用框图与带箭头的连接线表示。

那么如果连接到输出的音源变化时怎么办呢，来看看这个使用按键控制连接的[demo](https://lig-dsktschy.github.io/wpapi-osc/3/)(点击链接前注意播放音量)。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823217765772200_99.png)

在表示AudioNode的方框间，在连接前没有箭头连接线。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823220931717800_67.png)

在连接时出现了箭头连接线。

像这样在Web Audio Editor中可以实时可视化的表示AudioNode的连接状态。

### AudioParamオブジェクトの確認

Web Audio API による開発では、AudioNode だけではなく、それぞれの AudioNode が持つ AudioParam オブジェクトも複数扱います。これもまた、複雑な内容になると、その時々の状態を把握することは困難でしょう。

Web Audio Editorは、各 AudioParam オブジェクトの value プロパティを一覧表示することで、この問題も解決してくれます。

実際に、Web Audio Editor によって各 AudioParam オブジェクトの value プロパティを確認してみましょう。先ほどの複数の音源を一度に出力するサンプル（リンク先は音が出ます）を再度ひらき、今度は音源となる AudioNode のボックスをクリックしてみてください。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823224650594300_42.png)

クリックされた AudioNode のボックスが青くなり、「プロパティ」という欄が表示されましたでしょうか。

これが、クリックされた AudioNode の持つ AudioParam オブジェクトの value プロパティ一覧です。この場合では、OscillatorNodeの持つtype.value, frequency.value, detune.value が表示されています。

またここでは、別の AudioNode のボックスをクリックし、それぞれの frequency.value に別の値が設定されていることも確認してみてください。

では、AudioParam オブジェクトの value プロパティを変動させてみるとどうなるでしょうか。これまでの内容に、レンジバーによる音量調節機能を加えたサンプル（リンク先は音が出ます）で確認します。

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/11/147823226271241100_56.png)

中間処理を表す AudioNode が追加されていることを確認できたら、そのボックスをクリックしてみてください。この場合では、GainNode の持つ gain.value が表示されたかと思います。

次に、いま value プロパティを確認した AudioNode に対応するレンジバーを左右させ、gain.value を調節してみてください。そして、再度同じボックスをクリックすると、gain.value の表示が調節後の値に更新されることを確認できるはずです。

このように、Web Audio Editor は AudioParam オブジェクトの value プロパティに関しても、その時々の状態を表示してくれます。ただし、AudioNode の接続状態と違って、リアルタイムに反映されないことに注意してください。

AudioParam オブジェクトの value プロパティの表示は、ボックスがクリックされたタイミングで、現在の値に更新されます。

## まとめ

自分で作成したページだけでなく、既存のページをWeb Audio Editorで検証することももちろん可能です。

Web Audio APIを用いたページの開発、そして分析にも、Web Audio Editorは大きな助けとなります。どんどん活用していきたいですね。

ではまた！　つっちーでした。
