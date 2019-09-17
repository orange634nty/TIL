ruby tips
---

## ActiveSupport

ActiveSupportでは `slice` や `except` 、 `compact` 、 `reverse_merge` が使えるようになる

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

## セッターメソッドを呼ぶ時はselfを省略出来ない

参考：https://qiita.com/akira-hamada/items/4132d2fda7e420073ab7

## <code>`</code> について

コマンドとして実行されるようです

詳細は
https://docs.ruby-lang.org/ja/latest/doc/spec=2fliteral.html
の「コマンド出力」を参照

バックスラッシュ記法や式展開にも対応しています。 

## rubyのhashのarrayで特定のkeyの配列を取得する

つまり

```ruby
> hoge = [{a: 1, b: 2}, {a: 21, b: 22},{a: 11, b: 12}]
=> [{:a=>1, :b=>2}, {:a=>21, :b=>22}, {:a=>11, :b=>12}]
> hoge.map{ |h| h[:a] }
=> [1, 21, 11]
```

これはこんなふうにもかける

```ruby
> hoge.each_with_object(:a).map(&:[])
=> [1, 21, 11]
```

あんまり変わらないか…

参考：[第３弾！知って得する12のRubyのトリビアな記法](http://melborne.github.io/2012/04/26/ruby-trivias-you-should-know/)

## try と &.

try : メソッドを呼び出せる時に呼び出す  
&. : nil 出ない時に呼び出す

```ruby
foo.try(:hoge) # => nil
foo&.hoge # => error
```

参考：[Ruby の &. と #try の違い](http://secret-garden.hatenablog.com/entry/2016/09/02/000000)
