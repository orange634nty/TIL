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

例えばcostを二倍にしたものを出力したい場合は

```console
$ sed -e '1d' hoge.csv | awk -F"," '{print $1","$2","$3*2}'
1,apple,200
2,orange,300
3,grape,400
4,pinapple,240
```

名前にサフィックスをつけたい場合は

```
$ sed -e '1d' hoge.csv | awk -F"," '{print $1","$2"-hoge,"$3}'
1,apple-hoge,100
2,orange-hoge,150
3,grape-hoge,200
4,pinapple-hoge,120
```

## 特定の行の最大・最小・合計・平均を求める

costの最大・最小・合計・平均をawkを使って求めます

```
# 最大
$ sed -e '1d' hoge.csv | awk -F"," '{if(m<$3) m=$3} END{print m}'
200
# 最小
$ sed -e '1d' hoge.csv | awk -F"," 'BEGIN{m=100000}{if(m>$3) m=$3} END{print m}'
100
# 合計
$ sed -e '1d' hoge.csv | awk -F"," '{m+=$3} END{print m;}'
570
# 平均
$ sed -e '1d' hoge.csv | awk -F"," '{m+=$3} END{print m/NR;}'
142.5
```

参考：http://leetmikeal.hatenablog.com/entry/20130117/1358423717
