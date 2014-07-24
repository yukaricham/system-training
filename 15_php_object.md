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

## 定数
