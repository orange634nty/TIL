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

## スクロールのパララックス

vueでの実装方法

### イベントの追加

https://qiita.com/SatoTakumi/items/d88df8afae82c53d2d2a

```html
<div id="app">
  <div class="content">
    <span>{{ scrollY }}</span>
  </div>
</div>
```

```js
new Vue({
  el: '#app',
  data: {
    scrollY: 0
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
        this.scrollY = window.scrollY;
    }
  }
})
```

`addEventListener` にスクロールを検出した時に発火させるメソッドを追加

### `$refs` で直接要素を取得

https://codingexplained.com/coding/front-end/vue-js/accessing-dom-refs

```vue
<button ref="myButton" @click="clickedButton">Click Me!</button>
```

```js
new Vue({
	el: '#app',
	data: {
		message: 'Hello World!'
	},
	methods: {
		clickedButton: function() {
			console.log(this.$refs);
			this.$refs.myButton.innerText = this.message;
		}
	}
});
```

要素が表示させるし、ボタンの文字が `Hello World!` に変わる

### cssを変更する

```js
this.$refs.topImg.style['margin-top'] = // 変更する値を入れる・この時 `String` で入れること
```

これで多重スクロールするはず
だけど大変だからライブラリ使った方がいいと思う。

- https://parashuto.com/rriver/development/scroll-effect-library-scrollreveal

