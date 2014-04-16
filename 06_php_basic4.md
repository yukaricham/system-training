6章：PHPの基礎4
===

# Webサービスにおけるデータの受け渡し
Webサービスにおいて、画面間でのデータの受け渡しは必須です。例えば、一般的なユーザー登録画面は以下の様な画面遷移をします。

1. ユーザー情報入力フォーム
- 確認画面
- 登録完了

このような画面遷移を作る際、画面間でデータを引き渡す処理が必要になります。本日はそのデータの受け渡しの処理をやっていきましょう。

## Formタグを使ったデータの引き渡し

それではまずHTMLを記述してみましょう。最初はフォームを作成するHTMLをやります。

```html
<html>
  <head>
    <meta charset="UTF-8">
  </head>
  <body>
    <h2>入力フォーム</h2>
    <form action="confirm.php" method="post">
      <input type="text" name="email" />
      <input type="text" name="tel" />
      <input type="submit" value="登録" />
    </form>
  </body>
</html>
```

このようにして作ります。こちらのファイルは```input.php```という名前で保存しておきましょう。

## Formからデータを受け取る（POST)
このようにフォームタグに入力されたデータは、```<form action="xxxxx.php">```で指定されたURLに対してデータを引き渡すことができます。上記の例ですと、```confirm.php```というファイルへデータを引き渡していることになります。

それでは、```confirm.php```でデータを受け取りましょう。以下のようにして受け取ります。

```php
<?php
$email = $_POST['email'];
$tel   = $_POST['tel'];

echo $email . '<br />';
echo $tel . '<br />';
?>
```

このようにして前画面からのデータを受け取ることができます。```$_POST```という記述はPHPでの決まりだと思ってください。

上記の例ですと、```$_POST['email']```みたいにしてデータを受け取っています。この```email```の部分が、```<input type="text" name="email">```の```name="..."```の部分と対応します。このようにして、input.php側で定義したデータをconfirm.php側で受け取ることができます。

## Formからデータを受け取る（GET）

```html
<html>
  <head>
    <meta charset="UTF-8">
  </head>
  <body>
    <h2>入力フォーム</h2>
    <form action="confirm.php" method="get">
      <input type="text" name="email" />
      <input type="text" name="tel" />
      <input type="submit" value="登録" />
    </form>
  </body>
</html>
```

それでは今度は上記のHTMLを書いてみてください。ほぼ変更点はありませんが、１点だけ変わっている部分があります。```method="get"```の部分です。

それでは続いて、confirm.phpを以下のように修正してください。

```php
<?php
$email = $_GET['email'];
$tel   = $_GET['tel'];

echo $email . '<br />';
echo $tel . '<br />';
?>
```

同様に動いてると思います。ここで注目してほしいのはURLです。以下の様なURLになっていると思います。

http://fs01.local/xxxxxxxxxxxxxx/?email=xxxx&tel=xxxxxx

このように、```method=get```にすることでデータを受け渡す際にURL内にデータをいれて渡すようになります。一方で```method=post```ではURLにはデータは現れず、目に見えない裏側でデータを引き渡しています。

これはどちらも利用します。例えば、パスワードを入力するようなログイン画面などはURLに重要な情報が表示されてはいけません。そのようなときはPOSTを使うのが一般的です。

しかし、POSTだと裏側でデータが引き回されるため何らかの情報を他の人に渡すときなどは不便です。URL内にデータが入っているため、リンクを伝えるだけでデータごと引き渡すことができます。

このようにしてPOST/GETをそれぞれ使い分けて設計していたりします。

## 演習1
POSTでデータを渡してみよう。

```html
<html>
  <head>
    <meta charset="UTF-8">
  </head>
  <body>
    <h2>性別入力フォーム</h2>
    <form action="confirm.php" method="post">
      <label>男性</label>
      <input type="radio" name="gender" value="male" />
      <label>女性</label>
      <input type="radio" name="gender" value="female" />
      <input type="submit" value="登録" />
    </form>
  </body>
</html>
```

このHTMLを受け取って、男性をチェックしていたら男性と表示、女性をチェックしていたら女性と表示するプログラムを書いてください。

## 演習2
上記のプログラムをGETに変えてください


# 想定外の行動に対処する
ユーザーは我々の期待している通りに動いてくれません。プログラムを書く上でのコツは以下にして想定外の事例を考えることができるかという点です。

脆弱性（ぜいじゃくせい）もそうですし、意図せず謎の行動をとるユーザーもたくさんいます。分かりやすい例だと以下の様なことができてしまいます。例えば、先ほどのconfirm.phpへ直接アクセスするとどうなるでしょうか？

http://fs01.local/SystemTraining/2014/wadap/confirm.php

このように、エラーがでます。基本的にありえない動きではありつつも、それができてしまうという状態があることはプログラミングにおいて***バグ***と呼ばれます。今回の場合ですと、このようにして回避する必要があります。


```php
<?php

if (isset($_POST['email'])) {
  $email = $_POST['email'];
} else {
  $email = '';
}

if (isset($_POST['tel'])) {
  $tel = $_POST['tel'];
} else {
  $tel = '';
}

echo $email . '<br>';
echo $tel . '<br>';

?>
```

issetは値がセットされているのかをチェックするための関数です。このようにして、if文を使い値がセットされていたら〜というように条件分岐を書いてあげる必要があります。

サービス開発において、正常な処理だけつくることはあまり大変なことではありません。多くの処理がこのような想定外の行動に対応するための処理だったり、それを制御するための処理だったりします。それほど、ユーザーの自由な行動に対応するプログラミングというのは難しいものです。
