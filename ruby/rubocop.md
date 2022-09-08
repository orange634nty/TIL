Rubocop
---

Rubocop の実装を見るのが一番わかりやすいので、困ったら見よう！

https://github.com/rubocop/rubocop/tree/00e7ac78fb83383ef537e9e08ecf2301a1427578/lib/rubocop/cop

## カスタムルールの追加

- https://moneyforward.com/engineers_blog/2021/09/02/rubocop/
- https://docs.rubocop.org/rubocop/1.34/development.html

↑の記事はメソッドの呼び出し部分に対してチェックをしているので `on_send` を使用している

クラスの場合は `on_class` を使用する

### クラス名をチェック

デフォルトのrubocopでもクラス名の命名規則のチェックは行われています。  
なのでそこを参考にするといい → [class_and_module_camel_case.rb](https://github.com/rubocop/rubocop/blob/master/lib/rubocop/cop/naming/class_and_module_camel_case.rb)

```ruby
class Hoge < RuboCop::Cop::Base
  def on_class(node)
    name = node.loc.name.source  # これでクラス名を取得できる
    
    # 何かしらのチェックを行う

    add_offense(node.loc) # 問題がある場合に add_offense を呼ぶ
    # node.loc を使った方がクラス部分のみがハイライトされるので親切
  end
end
```

### 継承されたクラスの検証

継承したクラスは `nnode.parent_class.loc.node` で継承元のクラスのnodeを取得できる
あとは他のnodeと同じように検証ができる

例えば特定のクラスを継承している場合に警告を出すみたいにするには

```ruby
class Hoge < RuboCop::Cop::Base
  MSG = "dont use Hoge class for inheritance"
  def_node_matcher :user_hoge_class?, "(const ... :Hoge)"

  def on_class(node)
    parent_node = node.parent_class.loc.node 
    add_offense(parent_node) if user_hoge_class?(node)
  end
end
```

みたいになる

### AutoCorrect

```ruby
extend AutoCorrector
```

を追加したら使えるようになる

```ruby
class Hoge < RuboCop::Cop::Base
  MSG = "dont use Hoge.foo instead of Hoge.boo"
   def_node_matcher :use_hoge_boo?, '(send (const ... :Hoge) :boo)'

  def on_send(node)
    return unless use_hoge_boo?(node)
    add_offense(node) { |correct| corrector.replace(node.loc.selector, 'foo') }  # <= ここ！
  end
end
```

のようにブロックに定義できる
`replace` の第一引数には修正したい部分の `Parser::Source::Range`, `Comment` `RuboCop::AST::Node` を渡せばいい

### その他メモ

時間がある時にちゃんと調べるけど今は適当にメモしておく  
間違ってたらすみません

- `Parser::Source::Range`
  - ruby の構文解析でパースされた状態にもの
  - `source` でメソッド名などを獲得可能
  - add_offense に渡す時にRageが絞られて状態で渡すとハイライト箇所がその範囲になりそう？？？？
  - https://www.rubydoc.info/gems/parser/Parser/Source/Range
- `Parser::Source::Map::Constant`
  - 定数のソースマップ、クラスとかもここに属す
  - `constant.node` で node が取得できるのでマッチして検証する際は使用するといい
  - https://www.rubydoc.info/gems/parser/Parser/Source/Map/Constant
- `RuboCop::AST::ClassNode`
  - `on_class` で渡ってくる node
  - クラスに関する検証を行い場合はこれを使用する
  - https://www.rubydoc.info/gems/rubocop/0.69.0/RuboCop/AST/ClassNode
  - on_send の場合は `SendNode` が渡ってくる
  - どれも継承元は `RuboCop::AST::Node`
