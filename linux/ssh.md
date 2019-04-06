ssh
---

## known_host からホスト情報を削除する

直接ファイルを消すのもいいが、あんまりよくないのでコマンドから消した方がいい

```
ssh-keygen -R <消したいホスト>
```

参考：[known_hostからホスト情報を削除する](https://qiita.com/mobius01/items/133613e078df3137dafc)
