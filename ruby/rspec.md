rspec
---

＊ここのテスト周りのサンプルコードは自分で書いたものを使ったほうが良さそう

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
    expect(Japan.get_capital).to eq("Saitama")
  end
end
```

#### 参考

[Rspec で クラスメソッドのスタブを作る方法](https://qiita.com/Yinaura/items/dfc09fd6d4b953181e2d)

## インスタンス化したクラス全てに対してmockを使う

複数のインスタンスが生成されたり、実行中に生成されるインスタンスに対してmockを使いたい場合は `allow_any_instance_of` が使えます

**が**、公式のドキュメントでは使用を避けるようにと記載されています…

https://relishapp.com/rspec/rspec-mocks/v/3-1/docs/working-with-legacy-code/any-instance

自分も今後使うの避けようかなと思います…

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

## Factory_bot

元々は `FactoryGirl` という名前だった。  
なので、情報を調べるときは `FactoryGirl` でも調べた方がいいかも。

### 簡単な使い方

```ruby
describe Staffs, :type => :request do
  describe "GET index" do
    it 'スタッフデータ取得出来ている' do
      result = Staffs.find
      expect(result.id).to eq staff.id
    end
  end
end
```

こんな感じのテストを考える時、 `Staff` を `Factory_bot` でテストデータを作成する場合を考えます。  
まず、事前に `FactoryBot.define` でテストデータを定義しておきます。  
これは `spec/factories.rb` に定義します。

```ruby
FactoryBot.define do
  factory :staff do
    staff_last_name  "名字"
    staff_first_name "名前"
    staff_short_name "名字"
  end
end
```

次に先程のテストにテストデータを生成しましょう。

```ruby
describe Staffs, :type => :request do
  describe "GET index" do
    let!(:staff) { FactoryBot.create :staff } # <- 追記

    it 'スタッフデータ取得出来ている' do
      result = Staffs.find
      expect(result.id).to eq staff.id
    end
  end
end
```

`before` ブロックでもいいですが、私は `let!` を好んでよく使います。  
カラムの上書きも可能です（確か）


```ruby
describe Staffs, type: :request do
  describe "GET index" do
    let!(:staff) { FactoryBot.create :staff, staff_short_name: "あだ名"} # <- 追記

    it "スタッフデータ取得出来ている" do
      result = Staffs.find
      expect(result.id).to eq staff.id
    end
  end
end
```

##### 参考

- [RSpec + Factory_botでテストする方法](https://qiita.com/kkkkkkkkkk1005/items/9c957c38302eed8a5611)
- [Rails + RSpec で FactoryBot（旧 FactoryGirl）を使う](http://yurafuca.hatenablog.com/entry/2018/06/28/190842)

### 同一の内容のテストを行う場合は shared_examples_for を使うといい

条件が複数あって、出し分けがある場合はこれ使ったら楽  
https://qiita.com/etet-etet/items/7babe4856a1cd62b9ecb

```ruby
shared_examples 'Message send check' do
  # it ...
  # it ...
end

describe 'hoge hoge' do
  subject { hogehoge(foo) }
  it_behaves_like 'Message send check'
end
```

みたいなことが出来ます  
引数も渡せます

## timecop

https://qiita.com/tyamagu2/items/5f8dddfe079064b64d5e

rspecで時間関連を扱い場合に `timecop` を使うと、非常に簡単に時間を操作できます。

基本的に時間を止める `freeze` と、止めた時間を再び動かす `return` を使います。

```ruby:例
describe "sample test" do
  let!(:now) { Time.now } # now にしておくとnowをit等で使えるので色々便利
  before do { Timecop.freeze(now) } # 現在時刻で時間を止める
  after do { Timecop.return }
  it "check something" do
    # なんかする
  end
end
```

- Github：[travisjeffery/timecop](https://github.com/travisjeffery/timecop)
- 参考：[timecop 使ってみた](https://qiita.com/tyamagu2/items/5f8dddfe079064b64d5e)

## FactoryBotのtransient

transientはデータと関連しないアトリビュートを定義出来ます。  
例えば、付随するデータを作る、作らないみたいな分岐が出来ます。

```ruby
factory :user_account do
  transient do
    with_diary true
  end
  
  after(:create) do |user_account, evaluator|
    next unless user_account.with_diary
    # dairy情報を作成
  end
end
```

参考：[FactoryGirlのtransientとtraitを活用する](https://qiita.com/joker1007/items/da63b8630351c1f3fe1d)

## FactoryBotのbuildとcreateの違い

- build : メソッドはインスタンスをメモリ上にのみ記録する。
- create : メソッドはテストデータベースにも保存して、データを永続化させる。

イメージ的には Model.new は build、Model.create は create の関係である。

参考：[FactoryGirl: build と createの違い](http://tkymtk.hatenablog.com/entry/2013/12/15/214420)

## describe/context/it

[【Ruby on Rails】RSpecのdescribe/context/itの意味を理解した件](https://qiita.com/maeko/items/d7965be4adbeb2490229)

- `descirbe`：テスト対象、クラスやメソッド
- `context`：条件、丸々がない時とか
- `it`：検証内容、レスポンスがあるかとか、idが正しいかとか

## メソッドの呼ばれた回数をチェックする

`once` や `exactly(n)` などを使う

```
expect(some_class_instance).to have_received(:something).once
expect(some_class_instance).to have_received(:something).twice
expect(some_class_instance).to have_received(:something).exactly(3).times
```

注意が必要なのは 特定の引数が１回渡されるみたいな場合（例：ログよ呼び出してるか）

```
expect(some_class_instance).to have_received(:something).once
expect(some_class_instance).to have_received(:any)
```

みたいにすると、１回以上呼ばれていても `:any` なので問題なしになってしまう…

こういう場合は `and_wrap_original` を使って、呼ばれた引数をためて検証するのがいいはず…！

- https://techracho.bpsinc.jp/hachi8833/2018_04_02/54350
- https://relishapp.com/rspec/rspec-mocks/v/3-8/docs/configuring-responses/wrapping-the-original-implementation
