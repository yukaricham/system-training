10章：オブジェクト指向
===

## setterとgetter

クラス内に設定されているプロパティは、publicにすると直接触ることができますがprivateにすると触ることができないということをやりました。

```php
<?php
class Foo {
  public $public_val;
  private $private_val;
}

$a = new Foo();
$a->public_val  = "hogehoge"; // 問題ない
$a->private_val = "fugafuga"; // ここでエラーがでる
?>
```

上記のようなケースだとprivateで設定された値へアクセスすることができません。そういった場合に、以下のようにしてアクセス用のメソッドを作るようなケースがよくあります。

```php
<?php

class Foo {
  private $val;

  function set_val($a) {
      $this->val = $a;
  }

  function get_val($a) {
    return $this->val;
  }
}
```

Setter/Getterという使い方です。なんでこんなことをやるか。このあたりは設計思想にもよります。
様々な理由がありますが、内部的に使う変数を外から勝手に触らせないようにするというのが目的の場合が多いです。

例えば、とあるプロパティは配列を期待しているのに数値が入ってきたりしたらエラーがおきますよね。
そこで、Setter/Getterをかましてあげることで入ってきた値が妥当かどうかをチェックすることもできます。

このように外からアクセスさせないことをカプセル化と呼びます。

## コンストラクタ

コンストラクタとは、クラスをインスタンス化した時に自動的に呼ばれるメソッドです。以下のようにして使います。

```php
<?php

class Foo {
	function __construct() {
		echo "コンストラクタ呼ばれた";
	}
}

$a = new Foo();
// コンストラクタ呼ばれた
?>
```
上記を実行してもらうとわかると思いますが、本来ならメソッドとしてコールしなければいけないものが自動的に実行されています。このようにしてclassをインスタンス化したときに確実に実行させたい場合に使います。
また、```__construct()```メソッドでとる引数は、classをnewするときの引数が割り当てられます。

```php
<?php

class Foo {

    public $public_val;

    function __construct($val) {
        $this->public_val = $val;
    }
}

$a = new Foo('hogehogehoge');
echo $a->public_val;
?>
```

コンストラクタの使い方ですが、初期値などを設定したい場合につかったりします。指定した初期値がないと動作しないようなclassを設計する時、newする時点で初期値を持たせてあげるべきだからです。

## 演習１
コンストラクタで始まりの数値と終わりの数値を設定し、その間をすべて足し算するclassを作ってください。

```php
<?php

class Foo() {
  // いい感じに書く
}

$a = new Foo(1, 10);
echo $a->calc(); // 55
?>
```

## 演習２
上記のパターンをSetter/Getterを使って作ってください。（Getterは本来は不要ですけどね）

```php
<?php

class Foo {
  // いい感じに書く
}

$a = new Foo();
$a->set_start(1);
$a->set_end(10);
echo $a->calc(); // 55
?>
```

## 演習３
Fizz/Buzz問題をClassを使ってといてください。
