Illustrator script
---

イラレはスクリプトで操作可能  
ちょっと調べてみた

## リファレンス

公式：https://www.adobe.com/devnet/illustrator/scripting.html

でも大体以下の二つを読んでいた

- [Adobe Illustrator CC自動化作戦](http://www.openspc2.org/book/IllustratorCC/)
- [Adobe Illustrator Scripting Guide!](https://illustrator-scripting-guide.readthedocs.io/)

CC自動化作戦は逆引き、つまりやりたいことから検索出来て便利  
公式よりScripting Guideの方が見やすかったので、私はこっちで確認

## 悩んだこと

### 別名保存

`saveAs` の引数に `File` オブジェクトを突っ込む必要があるが、リファレンス見た感じない

http://chalcedony.hatenablog.com/entry/20140725/1406299387

```javascript
var fileobj = new File("ファイルパス");
```

とのことなので、これで上手くいった

### 画像の置き換え

CC自動化作戦には画像ファイルの扱いがなかったのでそうやるか悩んだ

http://chalcedony.hatenablog.com/entry/20090123/1232680836

どうやら `palcedItem` に入ってるみたい  
また、パスの入れ変えは


```javascript
placedItem.file = new File("ファイルへのパス")
```

で入れ替え可能
