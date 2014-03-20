2章：HTMLとCSSで組むレイアウト

===

# インライン要素とブロック要素

## ブロック要素
HTMLには様々なタグがありますが、大きく分けてインライン要素とブロック要素の2つに分類することができます。それでは実際に試してみましょう。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Title</title>
</head>
<body>
  <p>Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor.</p>
  <p>Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. </p>
  <p>Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium.</p>
</body>
</html>
```

それでは上記のHTMLを貼り付けて表示させてみましょう。```<p></p>```で囲まれた部分がそれぞれ改行されていると思います。このように、囲むことによって改行されるHTMLタグのことを **ブロック要素** と呼びます。それでは、わかりやすく背景色をつけてみましょう。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<style>
  #p1{
    background-color:blue;
  }
  #p2{
    background-color:red;
  }
  #p3{
    background-color:green;
  }
</style>
<title>Title</title>
</head>
<body>
  <p id="p1">Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor.</p>
  <p id="p2">Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. </p>
  <p id="p3">Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium.</p>
</body>
</html>
```

CSSでそれぞれのPタグに対して背景色をつけてみました。idの意味などについては後述します。このようにブロック要素はブラウザの幅に応じて最大幅まで広がります。そのため、そのままではブロック要素を横に並べておくことはできません。それでは続いてインライン要素を見てみましょう。

## インライン要素

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Title</title>
</head>
<body>
  <b>Lorem ipsum dolor sit amet</b>, consectetuer adipiscing elit. Aenean commodo ligula eget dolor.
</body>
</html>
```

今回はインライン要素として```<b></b>```タグを使用しました。このタグはBOLDの意味で、文字を太くするためのタグです。このように、インライン要素はその行の中で使われることが想定されているので改行されません。それではCSSで背景色をつけてみましょう。


```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Title</title>
<style>
  #b1{
    background-color:red;
  }
</style>
</head>
<body>
  <b id="b1">Lorem ipsum dolor sit amet</b>, consectetuer adipiscing elit. Aenean commodo ligula eget dolor.
</body>
</html>
```

背景色がついたのが確認できたと思います。このようにインライン要素は囲んだ領域のみた対象となり、横に広がることはありません。その名前の通り、インライン（行中）で使われることを想定されています。上記のもの以外には以下のタグもインライン要素です。よく使われるものの一部を紹介します。

|タグ名|用途|
|:--|:--|
|```<img src="..." />```|画像|
|```<a href="...">...</a>```|リンク|
|```<br />```|改行|
|```<span>...</span>```|意味付けをするだけ|

## セレクタ
CSSではセレクタというものをつかって、HTMLの指定した部分を装飾します。HTMLの中に、classとかidという表記がでてきますがそれをCSS側で指定してスタイルを適用することができます。まずよく使用される3つのセレクタを紹介します。


```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Title</title>
<style>
  h1{
    background-color:blue;
  }
  .p1{
    background-color:red;
  }
  #p2{
    background-color:green;
  }
</style>
</head>
<body>
  <h1>Title is here</h1>
  <p class="p1">paragraph is here 1</p>
  <p class="p1">paragraph is here 2</p>
  <p id="p2">paragraph is here 3</p>
</body>
</html>
```

それでは、```<style>...</style>```で囲まれた中を見て行きましょう。CSSの基本的な記述方法は以下のようにして記述されます。

```

セレクタ {
  プロパティ: 値;
}

```

ここで出てくるセレクタが、HTMLとの関連付けを表している部分です。まずセレクタは直接タグに対して指定をすることができます。上記のスタイルの場合は、このHTMLないに出てくるh1タグすべての背景色を青にするという意味になります。

小さなページならこれでも問題ありませんが、1つのタグに対してすべて同じデザインが適用されてしまうと困る場合が多々あります。そのような場合に、class/idを使用してタグに対してさらに別のラベリングをつけることができます。

HTML内で、id/classを指定する場合は以下のようにして記述します。上記の一部抜粋です。

```
  <p class="p1">paragraph is here 1</p>
  <p id="p2">paragraph is here 3</p>
```

このように、タグの中の要素として```class=...```や```id=...```という値をつけることでCSSから参照をすることができます。
それぞれのCSSからの参照方法は以下のようになります。

```
  .p1{
    background-color:red;
  }
  #p2{
    background-color:green;
  }
```

class指定したものは```.クラス名```、id指定したものは```#id名```というように表記をすることで指定した部分へスタイルを追加することができます。idとclassはそれぞれ似たようなことができますが、決定的な違いがあります。

同じid名はhtml内に1度しかつかってはいけない、classは何度つかってもOK、という点です。少量のCSSであればこのあたりは対して意識しなくても問題ないのですが、大量のCSSになってくるとidを使ったほうが良い場合、classを使ったほうがよい場合がそれぞれあります。

これはどちらかというと、デザインを再現するためにというよりも、このように設計したほうがあとからメンテナンスしやすいからという観点から選定されることが多いです。ちなみにnanapiでは原則idは使用しないという方針でHTML/CSSが組まれています。

## 上記以外のセレクタ
上記以外にも様々なセレクタがありますが、詳細の説明に関してはここでは割愛します。イメージしやすい例でいくと、マウスオーバーしたときのみに適用されるスタイルを定義したいときなどに使用することができるセレクタなどがあったりします。

こういったものを活用することで、よりメンテナンス性の高いHTML/CSSを構築することができるようになります。

## floatを使ったレイアウト
それでは、いままでの知識を踏まえた上で以下のレイアウトを組んでみましょう。

![Untitled.key.jpg](https://qiita-image-store.s3.amazonaws.com/222/10835/66acb1b8-d24b-0e0b-cf56-b0cc6f20e613.jpeg "Untitled.key.jpg")

このようなレイアウトを組む場合は、ブロック要素で大枠を作ってあげるのがセオリーです。このようなブロック要素で大枠を作る場合、```<div>...</div>```というタグを使います。

```<div>...</div>``` はdivisionの略で、具体的な意味を持つことはありません。HTMLを組む上で、意味的にまとめておきたいような場合に使ったりします。ここで1つ問題がでてきます。

ブロック要素は横に100%広がるという仕様でしたが、上記の例ですとContentとSideBarが横に並んでいます。このような場合はどのように書けば良いのでしょうか。

それでは以下のHTMLを見てください。結構ながい記述です。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Title</title>
    <style>
     #header{
       width: 960px;
       height: 150px;
       background-color:red;
     }
     #main{
       width: 960px;
     }
     #content{
       float: left;
       width: 660px;
       background-color:green;
     }
     #sidebar{
       float: right;
       width: 300px;
       background-color:yellow;
     }
     #footer{
       width: 960px;
       clear: both;
       background-color:blue;
     }
    </style>
  </head>
  <body>
    <div id="header">
    header
    </div>
    <div id="main">
      <div id="content">
        <h2>Content is here</h2>
        <p>this is paragrapth.</p>
        <p>this is paragrapth.</p>
        <p>this is paragrapth.</p>
        <p>this is paragrapth.</p>
        <p>this is paragrapth.</p>
        <p>this is paragrapth.</p>
      </div>
      <div id="sidebar">
        <h2>Sidebar is here</h2>
        <ul>
          <li><a href="#">list A</a></li>
          <li><a href="#">list B</a></li>
          <li><a href="#">list C</a></li>
          <li><a href="#">list D</a></li>
          <li><a href="#">list E</a></li>
          <li><a href="#">list F</a></li>
          <li><a href="#">list G</a></li>
        </ul>
      </div>
    </div>
    <div id="footer">
    footer
    </div>
  </body>
</html>
```

さて、急にHTML/CSSが増えてきました。実際に表示してみるとわかると思いますが、ブロック要素がよこに並んでいます。この並べるテクニックを紹介していきます。

ブロック要素を横に並べる方法の代表的なやり方として、floatというCSSのプロパティがあります。これをつかうことによって、ブロック要素を並べることができます。以下の記述です。

```
float: left;
```

上記の記述をすることで、対象となる部分が左寄せとなります。また、rightと指定することもできるのでcontentとsidebarを右寄せ・左寄せ位でそれぞれレイアウトを組んでいます。よく「回り込み」と呼ばれたりしますが、これはあまりよくない表現です。floatはその言葉の通り「浮く」というのが一番の特徴です。

古き時代はfloatではなく、2カラム構成はTableやframeなどで組んでいました。ご存知のとおり、htmlはレイアウトを組むための仕組みではないのでこれはあまり推奨されません。
