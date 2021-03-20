# wsl2 上で github pages に nuxt アプリをデプロイした時のメモ

## 開発環境の用意

wsl2(Ubuntu) でやります。

node のインストール。  
色々な方法がありますが、今回は流行の asdf を使ってみたいと思います。  
anyenv との違いがどういった物があるのか気になる所。

https://asdf-vm.com/#/core-manage-asdf みて、自分の環境を入力して、指示のままインストールします。  
https://github.com/asdf-vm/asdf-nodejs みて、必要な依存ソフトのインストール（既に全部入ってた）と plugin の追加を行います。

今回は最新版の LTS の 14.16.0 をインストール。

```
$ asdf install nodejs 14.16.0
```

終わったら `list` でちゃんとインストールされているか確認して、`global` に設定します。

```
$ asdf list nodejs
  14.16.0
$ asdf global nodejs 14.16.0
$ asdf reshim nodejs
```

エディタは VSCode を使います。  
Remote Development を使って VSCode で WSL 環境にリモート接続することができ、普通に windows のマシン上で開発するのと同じような感覚で扱えます。

https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack
https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl

この辺を入れれば OK です。

## nuxt の構築

https://ja.nuxtjs.org/docs/2.x/get-started/installation/ の指示に従って `npm init nuxt-app` を使っていきます。  
表示される質問等に答えていきます。  
この時今回は markdown で書きたかったので、`Nuxt/Content` を導入しています。

content は https://qiita.com/feb19/items/f030474fbdc4bcb4e0c7 を参考にして `index.vue` と `_slug.vue` を作成しました。

## github pages に github actions を使ってデプロイする

https://qiita.com/Ancient_Scapes/items/fe18bae043e4d35f1e39 を参考にして構築しています。  
`github-pages-deploy-action` は https://github.com/peaceiris/actions-gh-pages を使っています（ここはなんとなくこっちの方が使われてそうだったので）
