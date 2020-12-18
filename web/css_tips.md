css tips
---

## 斜めのページ

調べたけどちょっと難しいので一旦諦めた。  
けど、面白いので他のサイトでは挑戦したい。

- https://theorthodoxworks.com/web-design/slanting-background-css/
- https://coliss.com/articles/build-websites/operation/css/css-tutorial-slopy-elements-by-codrops.html
- https://tympanus.net/Tutorials/SlopyElements/index.html

## flex box

- https://ferret-plus.com/9420
- https://www.webcreatorbox.com/tech/css-flexbox-cheat-sheet

今回ちょっと普通cssフレームワークのグリッドと異なるので、フレームワークなしで独自実装してみた。  
一番シンプルなのだとこんな感じ

```css
.container {
  width: 100%;
}
.row {
  max-width: 1000px;
  margin: auto;
  display: flex;
  justify-content: center;
}
.col {
  width: 100%;
  margin: 0;
  padding: 10px;
}
```

```html
<div class="container">
    <div class="member-row">
        <div class="row">
            <div class="col">
                <!-- コンテンツが入る -->
            </div>
            <div class="col">
                <!-- コンテンツが入る -->
            </div>
        </div>
    </div>
</div>
```

この時`member-row`で背景を指定したりしてる。
こうすることで通常は端まで背景色がいくようにしている。

画像はここら辺を参考に調整。

- https://developer.mozilla.org/ja/docs/Web/CSS/Scaling_background_images
- https://developer.mozilla.org/ja/docs/Web/CSS/background-position

```css:基本
.member-row {
  background-image: url('/static/chara/hoge.png');
  background-attachment: fixed;
  background-position: center center;
  background-size: cover;
  background-repeat: no-repeat;
  background-size: auto 100vh;
}
```

```参考
background-size: auto 100vh;
                 ↑横幅 ↑縦幅
```

## 画像をぷるぷるさせる

参考 : https://q-az.net/buruburu-hurueru-css/
