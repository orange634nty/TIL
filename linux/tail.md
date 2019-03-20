tail
---

## `tail -f` を `grep` する

[リアルタイムに「tail -f」をgrepする方法](https://qiita.com/naotarou/items/ee2afc15804e37129c2d)

ログ見る時にgrepしたいと思ったので探したらあった

```
tail -f <hoge> | grep --line-buffered <boo>
```

## `tail -f` に色を付ける

上のの場合だと該当するやつ以外は表示されないのでなにかと不便…  
なので、`grep`したものだけを色付けしたいと思った。

[「tail -f」の出力の一部に色を付けて見やすくする](https://did2memo.net/2017/05/06/linux-tail-f-color/)

まんま同じことをした

```
tail -F ./path/to/log | sed -E 's/(error)/\o033[32m\1\o033[39m/g'
```

- `\033[32m` : 緑
- `\033[39m` : ？

他にもこういうツールを入れる手があるみたい

[linux(CentOS)のコマンドに色付け#tail -f コマンドに色をつける](https://qiita.com/ironsand/items/b308b3c689d69b94bae5#tail--f-%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AB%E8%89%B2%E3%82%92%E3%81%A4%E3%81%91%E3%82%8B)

> `sudo yum install multitail`
