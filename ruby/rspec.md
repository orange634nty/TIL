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
