Mac の OpenSSL が1.1以上になって、Ruby のインストールが上手くできなくなった（同様に mysql2 の gem も）
---

rbenv で ruby をうまくインストールできなくなってしまった。しばらく時間がかかったのでメモ程度に残しておきます。
原因としては下記記事とほとんど同じです。

[homebrew で openssl 1.0 がインストールできなくなっています - Qiita](https://qiita.com/kunit/items/0aef44d5e522abde1f9c)

同様のことが Ruby でも起こりました。
おそらく Ruby の暗号化周りが openSSL に依存している？らしくビルドする際にも発生します。自分がインストールしようとした Ruby のバージョンが古くopenSSL 1.0 にしか対応してませんでした。
また、これと同じ事が mysql2 の gem をインストールする際にも openSSL を正しく指定する必要があります。
ruby の openssl と mysql2 の openssl のバージョンを同じにしないとうまくインストールできません。
以上から手順をまとめると以下のような感じになります。

```
$ brew install rbenv/tap/openssl@1.0
$ RUBY_CONFIGURE_OPTS="--with-openssl-dir=`brew --prefix openssl@1.0`"
$ rbenv install <自分の欲しいバージョン>
```

また、 mysql2 の gem を入れる際も openssl@1.0 を指定しないといけません。bundler を自分の場合は使っていたので

```
$ bundle config --local build.mysql2 --with-ldflags=-L/usr/local/opt/openssl@1.0/lib --with-cppflags=-I/usr/local/opt/openssl@1.0/include
```

のようにオプションを追加しました。`.bundle/config` に

```
BUNDLE_BUILD__MYSQL2: "--with-ldflags=-L/usr/local/opt/openssl@1.0/lib --with-cppflags=-I/usr/local/opt/openssl@1.0/include"
```

のような設定が追加されていると思います。（ファイルに直接↑を指定してもいい）

この状態で

```
$ export LDFLAGS="-L/usr/local/opt/openssl@1.0/lib"
$ export CPPFLAGS="-I/usr/local/opt/openssl@1.0/include"
$ export PKG_CONFIG_PATH="/usr/local/opt/openssl@1.0/lib/pkgconfig"
$ bundle install
```

としたらうまく mysql2 の方もインストールできました。
