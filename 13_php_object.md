9章：オブジェクト指向

# PHPオブジェクト思考
前回、関数を定義するために```funcion```という機能をやりましたが、あれだけでは再利用などを行ううえでは若干不便です。

その問題を解決するために```class```という構造があります。

## class(クラス)

```php
<?php
class Foo {
	function hoge($a, $b) {
		return $a + $b;				
	}
}
?>
```

このようにclassを定義し、その中に```function```で関数を定義しておきます。このように、似たような機能などをclassでまとめておくことで使いやすくしたり、汎用性があがるというメリットがあります。作成されたクラスは以下のようにして実行します。

```php
<?php
class Foo {
	function hoge($a, $b) {
		return $a + $b;				
	}
}

$a = new Foo();
echo $a->hgoe(3, 5);
?>
```

まず、classをnewしてinstanceを生成します。classとは構造だけを表しているものなので、実体化してあげてから実行する必要があります。その実体化するために、newします。

そして、newしたことで生成されたinstanceから関数（メソッド）を呼び出します。```->```という演算子でそのインスタンスないから呼び出すことができます。

## Property(プロパティ)

```
<?php

class Foo {
	public $val;
}
?>
```

この```public $val```について学習しましょう。この```$val```というのは生成されたinstance自信が保持している変数です。以下の例を見てください。


```php
<?php

class Foo {
	public $val;
}

$a = new Foo();
$a->val = 'hogehoge';
echo $a->val; // hogehoge

$b = new Foo();
echo $b->val; // 空
?>
```

このように、それぞれのnewしたinstance内では使うことができます。しかし、newしたinstanceが別物になるとそこでは共有することができません。このようにして、instanceそのものに対して変数を持たせることができます。

また、```public```というのはnewしたinstanceの外から変数を設定できるようにするための定義になります。外部から設定されてしまうとこまるようなケースも多々あります。そのような場合は次のようにして使います。


```php
<?php

class Foo {
	private $val = 'hogefuga';
}


$a = new Foo();
$a->val = 'piyo';
?>

Fatal error: Cannot access private property Foo::$val in class.php on line 8
```

エラーメッセージのとおりですが、privateとして設定されたプロパティへはnewした外からは定義することができません。このようにすることで、newしたinstanceごとによって勝手に挙動を変えさせることを防ぐようにしています。

## method(メソッド)
さて、前半にもでてきましたがclassには機能を持たせることで様々な処理を行わせることができます。ここで前にやった、```function```を使います。以下のように定義します。


```php
<?php

class Foo {

	public $val;

	public function sum($a, $b) {
		$result = $a + $b;
		$this->val = $result;
	}
}

$a = new Foo();
$a->sum(4, 10);

echo $a->val;

?>
```

このようにして、```function```をつかってclass内にメソッドを定義することができます。また、そのメソッド内でclassの保持しているプロパティへアクセスすることもできます。上記の例は、```$val```というプロパティに対して足し算した結果を代入しています。

また、class内で自身のプロパティを参照したい場合```$this```を使います。newした場合はinstance化された変数を使いますが、class内では```$this```をつかうので注意しましょう。


## 演習

Hogeというクラスを作り、開始の値と終了の値をプロパティに持たせることで計算するようにしてください。利用イメージは以下のとおり。

``` <?php

class Hoge{
 // いい感じに書く
}

$a = new Hoge();

$a->start = 1;
$a->end   = 10;

echo $a->calc(); // 55
?>
```