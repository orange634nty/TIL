bundle tips
---

## bundle install すると mysql2 でエラーになる

https://qiita.com/tktcorporation/items/0ef8c930fc18ce72c301

自分は

```
bundle config --local build.mysql2 "--with-ldflags=-L/usr/local/opt/openssl/lib"
```

で OK だった

## --path が非推奨になってた

https://qiita.com/devzooiiooz/items/8babd82f780f01812f9d

これからは

```
bundle config set path 'vendor/gems'
```

にする必要がある
