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

## rake db:migrateで、uninitialized constant hogehoge

参考 : [xengineer’s diary - rake db:migrateで、uninitialized constant hogehoge](http://xengineer.hatenablog.com/entry/2014/12/08/_rake_db%3Amigrate%E3%81%A7%E3%80%81uninitialized_constant_hogehoge)

上記と全く同じ問題にぶち当たりました。  
ファイル名とクラス名が一致しないとダメよということ。  
私の場合はクラス名もファイル名もどちらも間違ってたという…

## exists?とpresent?の違い

[railsのARに対するpresent?とexists?のパフォーマンスの差](http://mikamisan.hatenablog.com/entry/2017/09/26/223137)

なので、`exists?` の方がよさそう
ただ、`present?` の方は `.first` つければ同じクエリにはなりそう…
チェックだけするなら`exists?` の方がスッキリ、チェックしたあとにその結果を利用するなら`.first.present?` の方がよさそう
