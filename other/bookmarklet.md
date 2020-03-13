book marklet
---

### 定型文挿入


下記はチャットワーク（かなり古いので今は使えないかも）の定型文

```js
javascript:s=new Date().toLocaleDateString()+' 日報\n・今日やったこと\n　- \n・明日の予定\n　- \n・困っていること、その他\n　- ';t=document.getElementById('_chatText');t.value=s;t.focus();t.selectionStart=t.selectionEnd=s.split('・明')[0].length-1;false;
```

見やすく複数行に
適当にコメント入れて。

```js
javascript:
// テンプレートの文字列
s = new Date().toLocaleDateString() + ' 日報\n・今日やったこと\n　- \n・明日の予定\n　- \n・困っていること、その他\n　- ';
// textarea取得
t = document.getElementById('_chatText');
// 挿入
t.value = s;
// フォーカスさせる
t.focus();
// キャレットの位置を移動させる
t.selectionStart = t.selectionEnd = s.split('・明')[0].length - 1;
// 呪文
false;
```

### 超簡易エディタ

ブラウザで書き込めるページを開ける

```js
data:text/html,<html contenteditable>
```
