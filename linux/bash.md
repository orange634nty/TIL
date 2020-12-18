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

逆に行頭を追加したい場合は以下のような方法で可能  
ただ、パイプラインだと出来ないので、やり方を要調査する

```
$ sed -e '1s/^/hoge\n/' hoge.csv
hogenid,name,cost
1,apple,100
2,orange,150
3,grape,200
4,pinapple,120
```

参考：https://qiita.com/U_ikki/items/b86ce318cb7c086bb6c1

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

### 特定の行を計算して出力する

例えばcostを二倍にしたものを出力したい場合は

```console
$ sed -e '1d' hoge.csv | awk -F"," '{print $1","$2","$3*2}'
1,apple,200
2,orange,300
3,grape,400
4,pinapple,240
```

名前にサフィックスをつけたい場合は

```console
$ sed -e '1d' hoge.csv | awk -F"," '{print $1","$2"-hoge,"$3}'
1,apple-hoge,100
2,orange-hoge,150
3,grape-hoge,200
4,pinapple-hoge,120
```

### 特定の行の最大・最小・合計・平均を求める

costの最大・最小・合計・平均をawkを使って求めます

```console
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

## 同じ行をカウントする

```csv:cost_list.csv
name,cost
orange,100
apple,120
pinapple,150
grape,100
strawberry,120
cherry,120
```

の時、同じコストがどれくらいあるか調査する

```console
$ sed -e '1d' cost_list.csv | awk -F"," '{print $2}' | sort | uniq -c | sort -n -k 1 | awk '{print "cost "$2" : "$1" items"}'
cost 150 : 1 items
cost 100 : 2 items
cost 120 : 3 items
```

| コマンド | 説明 |
|:---|:---|
| `sed -e '1d' cost_list.csv` | 行頭のカラム削除 |
| `awk -F"," '{print $2}'` | costだけ抜き出す |
| `sort \| uniq -c` | `uniq -c` で数を数えます<br /> `uniq` を使う際は先に `sort` する必要があるので `sort` しています<br />sortを使わない場合は連続した行しかuniqとして判定出来ないので、離れている行は正しく重複判定が出来ない<br />参考：https://www.soum.co.jp/misc/awk/3/ |
| `sort -n -k 1` | 見やすさの為に個数で降順に並び替えてます<br />参考：https://qiita.com/d-dai/items/b261fc8483d0cdeccb58 | 
| `awk '{print "cost "$2" : "$1" items"}'` | 見やすさの為にawkで出力を調整しています |

## aliasを無効にして実行する

alias を一時的に無効にするにはコマンドの前に `\` をつける  
今回は `rm` に `alias rm="rm -i"` を設定しているものとする

```console
$ ls
hoge.txt
$ rm hoge.txt
remove hoge.txt? n
$ \rm hoge.txt
$ ls
```

## 別ファイルのshellを読み込んで実行する（例えばbash_profileからbashrcを読み込む）

```
if [ -f ~/.bashrc ] ; then
    . ~/.bashrc
fi
```

のようにしたらいい

## 日付つきのファイルが欲しい

```
`date +%Y%m%d_%H-%M-%S`.log
```

みたいにすると「20170628_12-23-58.log」を得る
