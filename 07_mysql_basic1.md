6章：MySQLの基礎1
===

# 前回までの復習
- PHPをつかってPOST/GETでデータの受け取り
- $_GET/$_POSTなどでデータをPHPから参照

# MySQLを学ぶ
それでは前回までPHPを中心に学習してきました。しかし、PHPだけではデータを保存することや参照することはできません。そのためには、データベースという機構を学ぶ必要があります。

今回からはデータベースへのアクセス方法をがくしゅうしましょう。

## データベースとはなにか？
基本的には、データを保存するための機構です。ただしシステムにおいてデータベースと呼ばれる場合は一般的にRDBMSのことを指します

Relational Database Management Systemの略です。
基本的にはデータを保存する機能を提供するのがデータベースですが、複数のデータを連携させてデータを取得することができます。Excelでも似たようなことができますね。

http://ja.wikipedia.org/wiki/%E9%96%A2%E4%BF%82%E3%83%87%E3%83%BC%E3%82%BF%E3%83%99%E3%83%BC%E3%82%B9%E7%AE%A1%E7%90%86%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0

## なぜデータベースか？
Webサービスをつくるとき、データを保存しておく最も一般的な方法がデータベースに保存するという手法です。なぜ、データベースに保存する方法が一般的なのでしょうか？

それは、データの検索がしやすく、かつ安全に高速にデータを扱うことができるという点が挙げられます。Excelのように一人しか使わないような場合なら問題ありませんが、Webサービスのように常に大量のユーザーがアクセスしてくるような場合だとパフォーマンスが求められます。

そういった要件をさばくために有効な手法の一つとしてデータベースが挙げられます。

## データベースの種類
さて、データベースと一言にいっても様々なものが存在します。一般的によく使われているデータベースの一例を上げてみます。

- MySQL
- PostgreSQL
- MariaDB
- SQLite
- Oracle
- Microsoft Access
- SQL Server

他にもたくさんのデータベースがありますがよく名前をきくのはこの辺りです。ちなみに一部商用のものもあります。これはメーカーがつくり有料で提供されている製品です。

一方で、MySQLやPostgreSQLというのはオープンソースで開発されていて無償で使うことができます。その分、問題がなにか起きても基本的に自己責任です。ただし、ユーザー数が非常に多いので大体のよくあるトラブルは検索すれば出てきます。

nanapiでは、MySQLを利用しています。恐らく世界中もっとも使われているRDBMSでしょう。今回もMySQLを中心に学習をしていこうと思います。

## データベースのデータ管理方法
基本的なデータの管理方法は、Excelの表をイメージしてもらえれば大丈夫です。例えば、以下のようにしてデータが管理されています。

|id|firstname|lastname|gender|
|:--|:--|:--|:--|
|1|Shuichi|Wada|male|
|2|Takeshi|Tanaka|male|
|3|Ryota|Takeda|male|
|4|Ryoko|Sato|female|


データベースからデータを取得する際には、SQLという言語をつかって問い合わせます。これはRDBMSの種類が違っていても、ある程度同じように扱うことができます。今回はこのSQLを中心に学んでいきます。

# データベースにアクセスする方法
データベースの操作は基本的にコマンドラインで行います。
いわゆる「黒い画面」ですが、めげずにがんばりましょう。まず、Windowsの人は必要なソフトウェアがあるのでインストールしましょう。

## Windows
以下のPuTTYをダウンロードしてください
http://yebisuya.dip.jp/Software/PuTTY/

![system_study_06.pptx.jpg](https://qiita-image-store.s3.amazonaws.com/222/10835/d74e3e14-5986-8006-b395-21bc45971b65.jpeg "system_study_06.pptx.jpg")

ホスト名：lab103.rkst.jp

## Mac
ターミナルを立ち上げます

```
ssh dev@lab103.rkst.jp
```

## 共通

```
mysql -uroot -p
user dev;
```

# SQLを書こう
SQLで頻繁に行われる作業は以下の4種類です。

- データの参照（SELECT）
- データの保存（INSERT）
- データの更新（UPDATE）
- データの削除（DELETE）

それでは、それぞれの基本的な作業を実施していきましょう。

## データベース上でデータを扱うときに知っておくこと
データベースにおいて、データはTableという単位で保存されています。Tableという単位ごとに、きまった列のデータがありそれに応じてデータが保存されます。なお、今回は以下のように定義されているtableを使用します。データは参考としていれているだけなので気にしないでください。

各データのフィールド(id,firstname,lastnameなど)のことを ***Colum(カラム)*** と呼びます.

|id|firstname|lastname|gender|
|:--|:--|:--|:--|
|1|Shuichi|Wada|male|
|2|Takeshi|Tanaka|male|
|3|Ryota|Takeda|male|
|4|Ryoko|Sato|female|


## データの保存（INSERT)

```SQL
INSERT INTO users (firstname, lastname, gender) VALUES('taro', 'yamada', 'male');
```

SQLはこのようにして記述します。それでは一つづつちゃんと見て行きましょう。
以下のようにしてSQLは構成されています。

```SQL
INSERT INTO テーブル名 (対象カラム名, 対象カラム名, 対象カラム名) VALUES ('入力データ', '入力データ', '入力データ');
```

対象カラムの順番通りにVALUESの後ろに続くフィールドにデータを並べることで、そのカラムに対応したデータを並べます。
それでは続いて、INSERTしたデータを見てみましょう。


## データの取得（SELECT）

### 全件取得
```SQL
SELECT * FROM users;
```

データが全件表示されます。先ほど入力したデータが表示されているはずです。ターミナル内での表示になりますが、なんとなくデータが入っていることはわかるでしょう。

ここで気づいて欲しいポイントが、```id```カラムが入力していないのにちゃんと設定されている点です。これは、MySQL側の機能でそれぞれのデータが一意になるように付与してくれているIDです。これは絶対に重複することはありません。

このように重複することがなく、一意となるIDに値するもののことを ***PrimaryKey*** と呼びます。
一意という単語のことを、 ***ユニーク*** と呼ぶこともあります。これはどちらも「重複することがない」という意味なので注意してください。

### 条件指定してデータ取得
非常によく使います。以下のようにして条件を指定します。

```sql
;; ID指定で取得
SELECT * FROM users WHERE id = 3;

;; 名前指定で取得
SELECT * FROM users WHERE firstname = 'aa';
```

取得できたでしょうか。これはPHPのときに習ったifとにたように条件を組むことができます。以下のようにして複数条件を指定することもできます。

```sql
SELECT * FROM users WHERE firstname = 'aa' AND lastname = 'bb';
```

ORで指定することも可能です。
```sql
SELECT * FROM users WHERE firstname = 'aa' OR lastname = 'bb';
```

### カラム指定取得

```SQL
SELECT firstname, lastname FROM users;
```

このようにして、取得したいカラムを指定することができます。カラム数が多くなってきた時などに便利です。

### 順序指定

```sql
;; 昇順
SELECT firstname, lastname FROM users ORDER BY firstname ASC; // 
;; 降順
SELECT firstname, lastname FROM users ORDER BY firstname DESC;
```

```ORDER BY```を使うことによって、出力順序を指定することができます。またASC/DESCで昇順・降順をそれぞれ指定することができます。
