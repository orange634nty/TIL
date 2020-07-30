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

## node でシェルコマンドを実行する

`child_process` を使う  
自分の場合は扱いやすさてきに `execSync` を使うことが多い  
コマンド実行後の標準出力を返す

```js
const { execSync } = require('child_process')

const stdout = execSync('ls')
console.log(`stdout: ${stdout.toString()}`)
```

ファイルサイズが大きい場合は `spawn` を使った方がいい

参考: [シェルコマンドを実行する方法(child_process)](https://www.wakuwakubank.com/posts/728-nodejs-child-process/)

## 拡張子を省いたファイル名を取得する方法

めちゃめちゃ単純に `.` で split して後ろを取って、また繋げるだけ  
力技の方がシンプルにうまくいく場合が多い

```js
filename.split(".").slice(0, -1).join(".")
```

参考 : [How to trim a file extension from a String in JavaScript?](https://stackoverflow.com/questions/4250364/how-to-trim-a-file-extension-from-a-string-in-javascript)

## 正規表現を使ったマッチング

`RegExp` を使えばいい

```js
const regexp = new RegExp(`${name}-article.md`, "g")
const match_list = strBase.match(regexp)
```

参考 : [正規表現を使ったマッチングに変数を使用する](https://qiita.com/ykob/items/6e4d0b07bed57881a2bd)

## ファイルを扱う場合

`fs` を使うことになる

個人的には `readFileSync` と `writeFileSync` を積極的に使っていきたい。

参考 : [node.jsでファイルの入出力操作](https://qiita.com/shirokuman/items/509b159bf4b8dd1c41ef)

## 現在のディレクトリ名を取得する方法

Node.js標準でグローバル変数の `__dirname` から  
ディレクトリ名のみが欲しい場合は `path` モジュールを使うのがいい

```js
console.log(path.basename(__dirname))
```

参考 : [JavaScript/Node.jsで現在のディレクトリ名のみを取得する](https://qiita.com/Ancient_Scapes/items/6751461d8547200b6715)
