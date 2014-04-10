6章：PHP応用1
===

# PHPとMySQLの連携
これからは、PHPとMySQLの連携に入っていきます。以前にお話したように、Webサービスを作る上では様々な知識が必要になります。
前回までに学んだHTML/PHP/SQLの知識をもとにがんばりましょう。

## PHPからMySQLへ接続する
データベースに対してコマンドからSQLを発行していましたが、PHPと連携させる場合はPHPからSQLを発行することになります。
それでは、以下のコードを実行してみましょう。

```php
<?php

$mysql  = mysqli_connect('localhost', 'mysql', 'mysql', 'dev');
$sql    = 'SELECT * FROM users';
$result = $mysql->query($sql);

while($row = $result->fetch_assoc()) {
  echo $row['firstname'] . '<br>';
} 
?>
```

このようにしてPHPからMySQLに対してSQLを実行します。また、SQLが実行されたあとのデータはこのようにして受け取ってください。

## データの保存
保存は以下のようにして実行します。INSERT文を使うことでできます。S

```php
<?php

$mysql  = mysqli_connect('localhost', 'mysql', 'mysql', 'dev');
$sql    = 'INSERT INTO users (firstname, lastname, gender) VALUES ("hoge", "fuga", "male")';
$result = $mysql->query($sql);

?>
```

また、このようにすることでSQLの中に変数を入れることができます。

```php
<?php

$mysql  = mysqli_connect('localhost', 'mysql', 'mysql', 'dev');

$firstname = 'taro';
$lastname  = 'yamada';
$gender    = 'male';

$sql    = "INSERT INTO users (firstname, lastname, gender) VALUES ('$firstname', '$lastname', '$gender')";
$result = $mysql->query($sql);

?>
```

## 実習1

以下のフォームからデータを受け取って、MySQLのテーブルにINSERTしてください。

```html
<html>
<head>
  <meta charset="UTF-8">
</head>
<body>
  <h2>登録フォーム</h2>
  <form action="insert.php" method="post">
    <label>名前</label><input type="text" name="firstname" /> <br />
    <label>苗字</label><input type="text" name="lastname" /> <br />
    <label>男性</label><input type="radio" name="gender" value="male" />
    <label>女性</label><input type="radio" name="gender" value="female" /> <br />
    <input type="submit" value="登録" />
  </form>
</body>
</html>
```