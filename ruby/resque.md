Resque
---

ruby で使える非同期処理出来るやつ  
google に rescue と間違われる…  
Redis が必要なのでちょっと面倒

https://github.com/resque/resque

apiが気になったらこれ見たらだいたい分かる

https://www.rubydoc.info/gems/resque/toplevel

## tips

```ruby
# 登録しているResqueの一覧
Resque.queues

# 現在積んでるキューを確認する
# 引数指定しないと一番最初の queue のみを返す
Resque.peek("job_name")

# workerを確認する
Resque.workers

# 基本的な情報を確認する
Resque.info

# redis のデータを直接見る
# 格納されてるデータは list 型なので list 型のものは全て扱える
Resque.redis.llen("queue:<job_name>")
```
