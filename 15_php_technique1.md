11章：PHPいろいろ
===

## require
大規模なプログラムを書いていると1枚のxxx.phpというファイルがとにかく大きくなってしまい、扱いづらくなることが多々あります。
また、Classやfunctionなど様々な場所から呼び出したくなるような場面も多く出てきます。そういった場合に、PHPファイルから他のPHPファイルを呼び出すことができます。


index.php
```php
<?php

require 'module.php'

?>
```

module.php
```php
<?php

echo "hoge";

?>
```

このようにして、index.phpから、module.phpを呼び出すことができます。実際は、classやfunctionなどが定義してあるファイルを呼び出していろいろな場所からそのファイルを使うのがよくある使い方です。

index.php
```php
<?php

require 'foo.php'

$a = new Foo(1, 100);
echo $a->calc();

?>
```

foo.php
```php

<?php

class Foo{

  private $start;
  private $end;

  function __construct($s = 1, $e = 10) {
    $this->start = $s;
    $this->end   = $e;
  }

  public function calc($a, $b) {
    $sum = 0
    for ($i = $this->start; $i <= $this->end; $i++) {
      $sum += $i;
    }
    return $sum;
  }
}

?>
```

このようにしておくと、Fooというクラスの中で定義してある、1+2+3+...のような処理を行う内容は単独のファイルになっています。そのため、様々な場所からファイルを呼び出すことができます。
このように、できるだけ処理を共通化して、多くの場所から呼べるようにしておくことで似たような処理があった場合に再利用するということがよりやりやすくなってきます。


## 定数
プログラムの中で変わりうる値のことを変数と読んでいましたが、絶対にかわることのない値のことを定数と呼びます。たとえば、サイト名「nanapi」でなどはサイトないすべてで共通化されているべきものです。
そのように、どこからよんでも絶対に同じ値であることが保証されているものを定数と呼びます。

たとえば変数だと以下の様なことが起きてしまいます。

```php

<?php

$site_name = 'nanapi';

$site_name = 'hogehoge';

echo $site_name; // hogehoge

?>
```

このように、変数というものは同じスコープ内であれば上書きすることができます。よく考えて使わないとおおきなバグを生み出してしまう可能性もあります。そのようなことができなような仕組みが定数です。

```php

<?php
define('SITE_NAME', 'nanapi');
echo SITE_NAME;
?>

```

このように、```define```を使うことで絶対に変更できない値というものを定義することでサイト内で使いまわすことができます。大量の```define```だけしてるファイルをつくって、それを```require```するなどやったりします。
wp-config.phpを見てみましょう。wordpressの設定ファイルです。

wp-config.php
```php
<?php
define('DB_NAME', 'nanapi_blog');
define('DB_USER', 'nanapi_blog');
define('DB_PASSWORD', 'xxxxxxxxxxx');
define('DB_HOST', '192.168.20.20');
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');
define('AUTH_KEY',         'put your unique phrase here');
define('SECURE_AUTH_KEY',  'put your unique phrase here');
define('LOGGED_IN_KEY',    'put your unique phrase here');
define('NONCE_KEY',        'put your unique phrase here');
define('AUTH_SALT',        'put your unique phrase here');
define('SECURE_AUTH_SALT', 'put your unique phrase here');
define('LOGGED_IN_SALT',   'put your unique phrase here');
define('NONCE_SALT',       'put your unique phrase here');
```

このように、設定ファイルなどで多数利用されているのが定数という仕組みです。大きなサイトを作る際には必要な機構です。

## 関数を調べる
さて、ここまでくるとPHPの基本的な使い方はほぼ網羅したことになります。あとは、調べながらである程度のものはつくることができます。PHPの関数を調べる際は、このサイトをみて調べるのがよいでしょう。PHPの本家マニュアルです。熟練したエンジニアでも、すべての関数や仕様を把握しているわけではありません。
プログラムを書く、ということは調べながらでも問題はありません。なので、変に暗記しようとせずに積極的に調べながら書きましょう。

http://php.net/manual/ja/

## 演習１
掲示板をつくった時に定数化できる部分を定数化し、config.phpというファイルで別にしてください

## 演習２
Fizz/Buzz問題を定数をつかって
