npm-script
---

`package.json` の `script` に記述して、`npm run xxx` のような形式で実行するスクリプト  
glup や grunt などと比べると表現力に劣るが、学習コストが低く、node_module の資産を使える
glup/grunt おじさん（俗人化）を避けやすい

おまかな概要はこれがわかりやすい: [【2020年のタスクランナーはこれ！】npm scriptsを使ってみた【脱gulp】](https://hibi-update.org/javascript/npm-scripts/)

## ブラウザなどを開く

https://github.com/domenic/opener

ブラウザに飛んで開いてくれて便利

```
opener http://localhost:3000/
```

## 監視

https://github.com/open-cli-tools/chokidar-cli

babel 等はオプションで指定できるが、そういったものがない場合は cholidar-cli をつかうといい

```
chokidar article/*.md -c "./build.js"
```

`$SHELL` を環境変数にセットしてないとうまく動かないので、指定する必要がある

[Error $SHELL environment variable is not set](https://github.com/kimmobrunfeldt/chokidar-cli/issues/62)

## 複数の処理を実行したい

linux なら `&&` や `&` がありますが、 windows などはないので複数プラットフォームで使う際はこれがいい  
また、 `*` でパターンで scrupt を指定できて表現力が高い

https://github.com/mysticatea/npm-run-all

```
# 直列
run-s watch viewer

# 並列
run-p watch viewer
```

その他ツールはこちら参照 : [npm-scripts で使える便利モジュールたち](https://qiita.com/mysticatea/items/12bb6579b9155fd74586)

