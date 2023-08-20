Van.js
---

[Van.js](https://vanjs.org/)

Ractive にかける小さいライブラリ  
ビルドなどが必要なく単独で動く  
CDNから読み込むことでも使える

ReactやVue使うほどではないけど、バニラやJQueryは…って時に使えそう

一応 SSR にも対応しているバージョンもある  
node.http 使ってるのはいいなと思った

公式が出してる？解説の動画なのも今ぽい

## 雑感

- 宣言的にもかけるけど `van.add` のように直接 DOM を操作をできるので好みが分かれそう
- js 書き慣れてるならなんとなくでもなんとかなる
- hyperapp に似ているけど、Vna.js の方が js ぽい印象をうけた
  + hyperapp は変数、処理、domと完全にわかれていてフレームワーク感あったけど、Vna.jsはライブラリって感じの印象がある

## tips

### オリジナルのタグで要素をくくりたい

```js
const redText = (childElement) => {
  return p({class: "text-red"}, childElement)
}

redText("このテキストは赤くなります")
// => <p class="text-red">このテキストは赤くなります</p>
```
