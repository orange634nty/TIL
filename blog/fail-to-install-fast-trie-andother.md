fast_trie がエラーでインストールできない
---

先日 `bundle install` したところ以下のようなエラーが出ました

```
Building native extensions.  This could take a while...
ERROR:  Error installing fast_trie:
	ERROR: Failed to build gem native extension.
```

ちゃんと確認した感じ `fast_trie` というパッケージをインストールする際に発生しているようです。ちゃんとエラーを確認すると…

```
compiling trie.c
trie.c:84:8: error: implicit declaration of function 'trie_has_key' is invalid in C99 [-Werror,-Wimplicit-function-declaration]
    if(trie_has_key(trie, (TrieChar*)RSTRING_PTR(key)))
```

のようなエラーが出ています。これは C99 というISOで定められたC言語の規格に違反している際に出るエラーです。つまり、構文エラーではなくビルドすることはできます。以前は出てなかったのですが、mac をアップデータした際にコンパイラがアップデートしたのだと思います。

本当はこういったエラーがないバージョンに上げる必要がありますが、厳し場合もあると思います。一旦このエラーを無視してビルドすることにしましょう。`--with-cflags=-Wno-error=implicit-function-declaration` というオプションを付かけることで無視することができます。

```
$ bundle config --local build.fast_tire --with-cflags=-Wno-error=implicit-function-declaration
$ bundle install
```

同様のものが `thin` という gem でも発生したのた同様に対応しました。
