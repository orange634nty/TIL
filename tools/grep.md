grep
---

## 複数の検索対象をgrepで調べる

`-e` で複数指定する

```
grep -e bar -e foo
```

## リアルタイム tail -f を grep する

参考：[Qiita - リアルタイムに「tail -f」をgrepする方法](https://qiita.com/naotarou/items/ee2afc15804e37129c2d)

```
tail -f XXXXX | grep --line-buffered "YYYY"
```

## gzファイルをgrepしたい

過去のログファイルはgzに圧縮されることが多い
grepするには `zgrep` を使えば出来る

```
zgrep "key_word" kako.log.gz
```

参考：[Qiita - gzのファイルを展開せずにgrepする]https://qiita.com/CTFman/items/7b56b2f5c3073f8f6b19
