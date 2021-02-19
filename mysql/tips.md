tips
---

## テーブル情報を確認する時は`desc`より`show create table`

`show create table` の方が `desc` より情報が多い。
例えばインデックスやエンジンの情報が確認出来るのでそちらの方がいい。

参考：[MySQL :: MySQL 5.6 リファレンスマニュアル :: 13.7.5.12 SHOW CREATE TABLE 構文](https://dev.mysql.com/doc/refman/5.6/ja/show-create-table.html)

## エラーログの出力されるディレクトリ

`my.cnf` に `log-error=ぱす` で設定されている

https://qiita.com/toshihirock/items/a97d174be68f485fbbf2

`my.cnf` があるディレクトリは

```
mysql --help | grep my.cnf
```

で確認可能

https://qiita.com/is0me/items/12629e3602ebb27c26a4

## リレーログ

https://gihyo.jp/dev/serial/01/mysql-road-construction-news/0053

スレーブのみの生成されるログ、マスターからのバイナリログの情報を一旦書き込むリレーログファイル

## schema のダンプのみ取る

`-n` オプションでスキーマのみ取る

```
mysqldump -u hoge -p -d -n > shema.dump
```

## ２つのテーブルどちらにもあるIDを抽出

例えば２つのテーブルが合ってどちらも `user_id` を持つ時、どちらのテーブルにある `user_id` を抽出する方法は

```
SELECT auther.user_id
FROM auther
LEFT OUTER JOIN reader
ON auther.user_id = reader.user_id
WHERE reader.user_id IS NOT NULL
```

で求められる
