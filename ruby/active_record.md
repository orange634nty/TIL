Active Record
---

## belongs_to と has_one

`belongs_to` は他のモデルとの一対一の関連付けを行います  
`has_one` も同様に他のモデルとの一対一の関連付けを行います

ただ、 `hase_one` の場合は他方のモデルの方をまるごと含んでる必要があります。  
なので例えば

```ruby
class Book < ApplicationRecord
  belongs_to :author
  belongs_to :publisher
end
```

みたいな場合は `Auther` クラスで `has_one` として `:book` を指定する事ができません。

参考：[Active Record の関連付け (アソシエーション)](https://railsguides.jp/association_basics.html)


