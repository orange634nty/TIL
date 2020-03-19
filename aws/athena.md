aws athena
---

### 注意点

**とりあえず、パーテションを確実に入れる**

これだけは守れば多分大丈夫

### stringになってるjsonのデータから抽出する

正規表現から取得するのもありだが、jsonなら `json_extract` という関数を使うことでパース可能です。

例えば、`request` というカラムがjsonを持ち

```json
{ "name": "むさし", "id": "orange634nty", "lang" : "japanese" }
```

みたいな構造のデータが入ってるとします。
この時 `name` の値を抽出するには

```sql
json_extract(param, "$.name")
```

のように書く必要があります。

参考 : [JSON からのデータの抽出](https://docs.aws.amazon.com/ja_jp/athena/latest/ug/extracting-data-from-JSON.html)

### 正規表現

正規表現は `regexp_extract` と `regexp_like` を使うことが多い

`regexp_extract` はマッチした値の抽出、`regexp_like` はマッチしたパターンの判定を行います。

### 他の型へのキャスト

`CAST ( expression AS type )` を使います。  
特に、上記の **stringになってるjsonのデータから抽出する** で抽出されたものは string なので int 等に変換したい場合に有用です。

参考 : [配列のデータ型の変換](https://docs.aws.amazon.com/ja_jp/athena/latest/ug/converting-array-data-types.html
