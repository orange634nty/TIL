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

## `Time.now.between?(hoge, fuga)`

ActiveSuportの機能  
ruby標準ではないみたいなので注意

https://apidock.com/rails/ActiveSupport/TimeWithZone/between%3F

ちなみに

```
Time.now.between?(yesterday, nil)
```

は`ArgumentError`が発生する

## 再代入

値があったらその値を返して、ない場合は値を算出して返すのような時

```ruby
def get_param
  return @param if @param
  @param = DB.get_param
end
```

みたいにするより、

```ruby
def get_param
  @param ||= DB.get_param
end
```

`||=` を使った方が完結でわかりやすい

## `||`の挙動

rubyでは`||`は前の評価、後ろの評価の順で評価を行って、trueならその値を返すみたいです。

```
irb(main):001:0> a = 1
=> 1
irb(main):002:0> b = 2
=> 2
irb(main):003:0> a || b
=> 1
irb(main):004:0> b || a
=> 2
irb(main):005:0> c = nil
=> nil
irb(main):006:0> c || a
=> 1
irb(main):007:0> c || nil
=> nil
irb(main):008:0> c || false
=> false
```

なので、もし◯◯◯ならA、違うならBみたいな、デフォルト値をもたせる動きの時に使えます

```ruby
def user_static_num
  A.num || B::STATIC_NUM
end
# A.numは有効な場合はその値、無効な場合はnilを返します。
```

## rubyのcase

rubyのcaseでは複数の値が設定することが出来るみたい。

配列の展開と組み合わせて使うことが可能

```ruby
febo = [1, 2, 3, 5, 8, 13]
perfect_num = [6, 28, 496, 8128]
case target_num
when *(febo)
  puts "#{target_num} is febo num."
when *(perfect_num)
  puts "#{target_num} is perfect num."
else
  puts "#{target_num} is normal num."
end
```

## Railsにおけるエラーの記述方法

https://blog.toshimaru.net/ruby-standard-error/

> タイトルの通り、Rubyで独自例外を定義するときは`Exception`ではなく、`StandardError` を継承するしきたりとなっています。

railsの例だけど、padrinoも同じみたい

## hashでデフォルト値を使う方法

`fetch`というメソッドがある

```
hash.fetch(:key_not_exist_in_hash, DEFAULT_PARAMATER)
```

参考 : [ハッシュの安全な扱い方 (デフォルト値とその落とし穴について)](https://qiita.com/QUANON/items/bcd3f0c877796b8be7e1)
