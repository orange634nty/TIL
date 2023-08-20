router
---

公式：https://router.vuejs.org/ja/guide/

vue-router.js を特に理由なければ使用することが多いと思う

## routerでurlに `#` がつかないようにする

```javascript
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

のように `mode: 'history'` を設定すればOK

http://den2sn.hatenablog.com/entry/2017/06/22/120018
