aws athena
---

### 注意点

**とりあえず、パーテションを確実に入れる**

これだけは守れば多分大丈夫

### stringになってるjsonのデータから抽出する

正規表現から取得するのもありだが、jsonなら `json_extract` という関数を使うことでパース可能です。

参考 : [JSON からのデータの抽出](https://docs.aws.amazon.com/ja_jp/athena/latest/ug/extracting-data-from-JSON.html)
