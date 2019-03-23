padrino
---

## padrion内で独自エラーの継承元

[Rubyで独自例外を定義するときはStandardErrorを継承する](https://blog.toshimaru.net/ruby-standard-error/)

> タイトルの通り、Rubyで独自例外を定義するときは`Exception`ではなく、`StandardError` を継承するしきたりとなっています。

railsの例だけど、padrinoも同じように `StandardError` を継承した方がいい。
