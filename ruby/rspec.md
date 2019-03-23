rspec
---

## mockの使い方

```ruby
# japan.rb
class Japan
  def get_capital
    "Tokyo"
  end
end

# japan_spec.rb
require_relative "japan.rb"

describe "Japan.get_capital" do
  it "returns Saitama" do
    japan = Japan.new 
    allow(japan).to receive(:get_capital).and_return("Saitama") 
    expect(japan.get_capital).to eq("Saitama")
  end
end
```

- `allow`：引数にスタブ化したいメソッドを持つクラスを突っ込む
- `recieve`：引数にスタブ化したいメソッド名のシンボル
- `and_return`：引数にスタブ化したメソッドの戻り値

mockなどを使うとDBへのアクセスが減るのでテストが早くなる。

#### 参考

- [使えるRSpec入門・その3「ゼロからわかるモック（mock）を使ったテストの書き方」](https://qiita.com/jnchito/items/640f17e124ab263a54dd)
- [allow、receive、and_return メソッドを使って特定のメソッドをスタブ化する](https://qiita.com/suzuki86/items/5549d5fab231a907642d)

## クラスメソッドでmockを使う

上の例だとインスタンス化したやつをallowの引数に入れましたが、ここに対象のクラスメソッドを持つクラスを入れます。

```ruby
# japan.rb
class Japan
  def self.get_capital
    "Tokyo"
  end
end

# japan_spec.rb
require_relative "japan.rb"

describe "Japan.get_capital" do
  it "returns Saitama" do
    allow(Japan).to receive(:get_capital).and_return("Saitama") 
    expect(japan.get_capital).to eq("Saitama")
  end
end
```

#### 参考

[Rspec で クラスメソッドのスタブを作る方法](https://qiita.com/Yinaura/items/dfc09fd6d4b953181e2d)

## rspecで使うマッチャー

[使えるRSpec入門・その2「使用頻度の高いマッチャを使いこなす」](https://qiita.com/jnchito/items/2e79a1abe7cd8214caa5)

基本的に`to`や`raise_error`を使う感じでいく。  
気をつけないと行けない点は、true/falseの判定です。  
厳密に`true/false`の判定したい時は`be_ture/be_false`を使うのは不適切

というのも`be_ture/be_false`は

```ruby
expect(1).to be_true
expect(nil).to be_false
```

のテストが通ってしまうのです！

```ruby
expect(true).to be true
expect(false).to be false
```

厳密に行うには上記のようにする必要があります。  
なので基本的には`be_true/be_false`は使わない。
