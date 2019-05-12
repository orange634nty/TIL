tips of node
---

## コマンドライン引数を取得する

参考：https://qiita.com/furusin_oriver/items/f030d1eaa9e7b54233c3

```
process.argv
```

で取得が可能
ただし、

```
node index.js hoge foo
```

のような場合は

```
[ '/path/to/node',
  '/path/to/index.js',
  'hoge',
  'foo']
```

のようになります。

## async を top levelで行いたい

参考：https://stackoverflow.com/questions/46515764/how-can-i-use-async-await-at-the-top-level

これは古き良きjsぽい感じで

```javascript
(async () => {
  await <非同期関数>()
})()
```

のようにやればいい
