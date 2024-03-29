8章：オブジェクト指向

# オブジェクト指向

## オブジェクト指向とは？

プログラミングを行う上での一つの考え方が、「オブジェクト指向」と呼ばれるものです。様々な考え方がありますが、そのなかでも最も定着して幅広く使われている考え方です。

このオブジェクト指向というのは、基本的には言語に依存するものではなくコードの書き方そのものについてなので、同じ言語を使ってもオブジェクト指向として書くこともできますし、そうではない書き方もできます。

http://ja.wikipedia.org/wiki/%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E6%8C%87%E5%90%91

## なぜオブジェクト指向か
プログラムの書き方はいくらでも自由に書くことができます。しかし、あまりにも自由に書いてしまうと度重なる仕様変更などについていくことがどんどんと困難になってきます。

また、似たような機能をバラバラに実装してしまうのも効率が非常に悪いプログラムになってしまいます。そのため、似ている機能を再利用できるようにしたりまとめておくような機構が必要になってきます。

ただし、どういう書き方や設計がオブジェクト指向らしいのか、という点は宗教論争に近いもので、様々な意見があります。そのため、まずは再利用するという機能の使い方から説明をしていきます。

## PHPにおける関数の再利用
まずは、自分で関数の定義をやってみましょう。PHPでは以下のようにして関数を定義することができます。

```php
<?php

function sum($a, $b) {
	$val = $a + $b;
	return $val;
}

$result = sum(3, 4);
echo $result;
```

この```function```というのは、自分で関数を定義するための機能です。いままで使っていた、```echo```などはもともとPHP側が用意している関数です。

このように、自分のプログラム内でよく使うような処理はこのようにして関数化しておくことでいつでも呼び出すことができます。このようにしてできるだけ同じような処理はまとめておくことが、あとあとのメンテナンスのしやすさにつながります。

## ユーザー定義関数の使い方

```php
<?php

function hoge($a, $b, $c) {
	return $a;
}

```

まず```function ...(){}```のfunctionに続く部分が、定義する関数名になります。このようにして名前をつけることができます。長くなってもよいので、できるだけわかりやすい名前をつけておいたほうがよいです。

```function ...($a...)```みたいになっている部分は、その関数内だけで使用される変数です。引数と呼ばれているもので、ここで順番されたとおりに呼び出すときも使います。

また、定義した関数内の変数と関数外の変数は別物です。以下の例をみてください。

```php
<?php

function hoge($a, $b) {
	$c = 10;
	return ($a + $b) * $c;
}

echo $c; // 参照できない

$c = 100;

function hoge2() {
	echo $c; // 参照できない
}
```

また、```return```をすることでその関数の結果を戻すことができます。returnがあった時点でその関数は終了するので注意してください。

```php
<?php

function hoge($a, $b) {

  if ($a == 0 || $b == 0) {
	return; // ここで処理が終わる
  }

  return $a + $b;
}
```

また、引数をとらない関数も定義できます。

```php
<?php

function hoge() {
	echo 'hogehoge';
}

hoge();
```


## 実習
以下のユーザー定義関数を作ってください

```php
<?php

function sum($start, $end) {
	// 処理を書く
}

echo sum(1, 10); // 1+2+3+...10の結果が表示される
```
