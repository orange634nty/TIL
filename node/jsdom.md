jsdom
---

https://github.com/jsdom/jsdom

js 制の dom を扱えるライブラリ

## 読み取る

readme に書いてるけどシンプルにやるなら

```js
const { JSDOM } = require("jsdom")

const { document } = (new JSDOM(html_str)).window
cnsole.log(document.querySelector("h1").textContent)
```

とするのがいい

## 編集・出力

```js
document.querySelector("title").textContent = "update title"
```

のようにすると値が変わります。
また、編集後の html を取得するには

```js
document.documentElement.outerHTML
```

としたらいい
