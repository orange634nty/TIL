tips
---

面倒なので、linuxに関わるツール類も一旦ここにまとめてしまう予定

## linux で peco を入れる

https://www.labohyt.net/blog/microsoft/post-2532/

バイナリを落として来て、パスが通ってるところに置くだけぽいが上手くいかない…  
これは素直に `go get` で入れてビルドするほうがバージョンアップできるからいいかもしれない

## フルパスの取得

```
readlink -f index.html
```

ただしmacでは使えない…

## freeの見方

https://www.khstasaba.com/?p=735

buffers/cache はシステムから割り当てられる領域なので見るときに注意
