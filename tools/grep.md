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
