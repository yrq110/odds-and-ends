# CSS中使用SVG制作选择框组件
***

>* 原文链接 : [JavaScript不使用！ SVGを使ってCSSでチェックボックスを作る方法](https://liginc.co.jp/315466)
* 原文作者 : [はやち](https://liginc.co.jp/member/member_detail?user=hayachi)
* 译者 : [yrq110](https://github.com/yrq110)

***

![](https://cdn.liginc.co.jp/wp-content/uploads/2016/12/14832784866283400_43-1310x874.jpg)


どうもですよ、はやちですよ₍₍ (ง ˘ω˘ )ว ⁾⁾

今回は、以前SVGのアニメーションでご紹介させていただきましたこちらのアニメーション（↓）を使ったチェックボックスの作り方を、ご紹介いたします( ˇωˇ)☝


## 実装方法

まずは実装方法を紹介します( ˇωˇ)☝

### マークアップ

SVG をインラインで label 内に入れます( ˇωˇ)☝

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

### スタイル

#### SVGとアニメーションの設定

SVG の初期設定とアニメーションの設定をします。

描かれるアニメーションをするために、線の間隔が全部埋まるまで stroke-dasharray を設定して、stroke-offset を同じ数値分指定して、線の位置が見えなくなるまで設定をします( ˇωˇ)☝

今回のアニメーションは、stroke-offset （線の位置）と stroke-opacity （線の透明度）を 0.3s 動かします( ˇωˇ)☝

```css
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
    fill: none; //塗りつぶしを消す
    stroke: #000; //線の色を設定
    stroke-linejoin:round; //パスのつなぎ目を丸くする
    stroke-linecap:round; //パスの端を丸くする
    stroke-dasharray: 51; //線の間隔を設定
    stroke-dashoffset:51; //線の長さを設定
    stroke-opacity:0; //線の透明度を設定
    stroke-width:4px; //線の太さを設定
    transition: stroke-dashoffset 0.3s ease, stroke-opacity 0.3s;
    //▲線の長さと線の透明度のアニメーション
  }
}
```
#### チェックボックスの設定

チェックボックスの疑似要素 checked で、アニメーション発火として使いたいので、label, svg, path 要素たちを、間接セレクタで設定します( ˇωˇ)☝

これで checked になったとき、stroke-dashoffset （線の長さ）と stroke-opacity （線の透明度）のアニメーションが発火されます( ˇωˇ)☝

```css
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

実際にできたものがこちらになります( ˘ω˘)☞三☞ｼｭｯｼｭｯ

<p data-height="265" data-theme-id="0" data-slug-hash="ZBYqyW" data-default-tab="css,result" data-user="Hayachi" data-embed-version="2" data-pen-title="SVG CheckBox" class="codepen">See the Pen <a href="http://codepen.io/Hayachi/pen/ZBYqyW/">SVG CheckBox</a> by Kayoko Hayashi (<a href="http://codepen.io/Hayachi">@Hayachi</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
