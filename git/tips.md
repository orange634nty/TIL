git tips
---

## ローカルのブランチ名を変更する

[gitのローカルのブランチ名を変更したい](https://qiita.com/suin/items/96c110b218d919168d64)

```
git branch -m <古いブランチ名> <新しいブランチ名>

# 今いるブランチ名を変更する時
git branch -m <新しいブランチ名>
```

## 間違えてaddしちゃった時

[git の add を取り消す](https://qiita.com/nabezokodaikon/items/7ee4900d28d8d863978e)


```
git reset HEAD <取り除きたいファイル名>
```

## コンフリクトしたから取り消したい

[【git】マージしたけどやっぱりやめたい時のやり方4種類](https://qiita.com/chihiro/items/5dd671aa6f1c332986a7)

コンフリクト修正するのをやめたい時

```
git merge --abort
```

他にも場合によって様々だけど自分は上のパターンが多い

## マージする

`branch-a` に `branch-b` をマージする

```
git checkout branch-a # <- マージ先に切り替える
git merge --no-ff branch-b # <- マージしたいブランチを入れる
# コンフリクトがある場合は直してaddしてcommit
```

## gitの追跡

`push`するときに`-u`オプションをつけると追跡する。

参考 : [ブランチを指定して git push する方法](
