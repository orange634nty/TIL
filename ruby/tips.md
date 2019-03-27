ruby tips
---

## ActiveSupport

ActiveSupportでは`slice`や`except`、`compact`、` reverse_merge`が使えるようになる

```ruby
some_hash = {
  key_a: "some content",
  key_b: "some content",
  key_c: "some content"
}

# :key_aと:key_bを取り出したい
some_hash.slice(:key_a, :key_b) #=> {key_a: ..., key_b: ...}

# :key_cを除外したい
some_hash.except(:key_c) #=> {key_a: ..., key_b: ...}

hash = { a: true, b: false, c: nil }
hash.compact # => { a: true, b: false }

options = options.reverse_merge(size: 25, velocity: 10)
# 以下のコードと等価
options = { size: 25, velocity: 10 }.merge(options)
```
[ActiveSupportのHash拡張であるslice, exceptがびっくりするぐらい便利](https://qiita.com/mah_lab/items/ed10bae99105ea2fd8bd)

## `Time.mday` と `Time.day` について

どちらも同じみたい  
他のメソッドの説明等では `mday` を使ってるので、 `mday` 使った方がいいように思う

参考：https://docs.ruby-lang.org/ja/latest/class/Time.html#I_DAY
