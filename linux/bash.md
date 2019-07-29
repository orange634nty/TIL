bash tips
---

## awkを使ってcsvファイルを処理する

以下のようなcsvファイルがあるとします。

```csv:hoge.csv
id,name,cost
1,apple,100
2,orange,150
3,grape,200
4,pinapple,120
```

### 先頭の行を飛ばす

csvの場合はカラムであることが多いので、消したいことが多いと思います。  
そういう時は以下の様にして取れます

```console
$ sed -e '1d' hoge.csv
1,apple,100
2,orange,150
3,grape,200
4,pinapple,120
```

参考：https://it-ojisan.tokyo/sed-d-command/

### 特定の行だけ抜き出したい

nameの一覧を作りたい時

```console
$ sed -e '1d' hoge.csv | awk -F"," '{print $2}'
apple
orange
grape
pinapple
```

結合する場合は

```
$ sed -e '1d' hoge.csv | awk -F"," '{print $2}' | tr '\n' ',' | sed s/,$//g
apple,orange,grape,pinapple
```

みたいに出来ます

- `tr '\n' ','` ： 改行を `,` に置き換える
- `sed s/,$//g` ： 最後の `,` を消す

参考：https://qiita.com/piroor/items/55ff672cb9f8e375e659

## 特定の行を計算して出力する


