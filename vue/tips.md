tips
---

## vueでキー入力をdiv要素でも使えるようにする

https://stackoverflow.com/questions/39176423/why-is-vue-js-key-modifier-only-working-for-button-and-not-div

ここにあるように `tabindex="-1"` にする。
するとkey入力も反応できる。

## vueでのforでkeyがない時

いつもやり方忘れるので。  
`(log, index)` のように受け取ると `index` が受け取れる。
これを `key` に指定する方法が一番簡単。
https://forum.vuejs.org/t/v-for-with-simple-arrays-what-key-to-use/13692

```js
<p for="(log, index) in logs" :key="index">{{ log }}</p>
```
