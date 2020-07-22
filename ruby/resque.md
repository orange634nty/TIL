Resque
---

ruby で使える非同期処理出来るやつ  
google に rescue と間違われる…  
Redis が必要なのでちょっと面倒

https://github.com/resque/resque

## tips

```ruby
# 登録しているResqueの一覧
Resque.queues

# 現在積んでるキューを確認する
Resque.peek("job_name")
```
