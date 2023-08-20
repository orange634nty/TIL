js tips
---

### カラーコードをRGBにする

https://teratail.com/questions/21946

```
const colorCode = "8f5c44"
const red = parseInt(colorCode.substring(0, 2), 16)
const green = parseInt(colorCode.substring(2, 4), 16)
const blue = parseInt(colorCode.substring(4, 6), 16)
```

### 背景色に合わせて見えやすい文字色にする

https://blanktar.jp/blog/2020/11/css-automate-foreground-text-color

ちょっと上手くいかない時もある

