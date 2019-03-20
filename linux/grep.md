grep
---

## `tail -f` を `grep` する

https://qiita.com/naotarou/items/ee2afc15804e37129c2d

ログ見る時にgrepしたいと思ったので探したらあった

```
tail -f <hoge> | grep --line-buffered <boo>
```
