# MicroBatchFramework

## version更新

### ver0.3

- logger周りが変わってたポイ

### ver0.4

- オプションなしで引数が使えるようになった
- マルチコマンド対応 `hoge foo` みたいなの

## 使ってみた

- Qiita : https://qiita.com/orange634nty/items/5bf8c73612a5d3fbc1db
- Github : https://github.com/orange634nty/micro-batch-test

### 学び

- `dotnet add package` でパッケージを入れても自動で依存解決してくれないみたい
  - その時は手動で追加した
- dotnet 2.2 だと、c# のバージョンはデフォルトだと 7.0 なので、自分で指定する必要があり
  - `.csproj` ファイルで `<LangVersion>7.3</LangVersion>` を追加
  - 参考 : [.Net CoreプロジェクトでC#のバージョンを変更する方法](https://qiita.com/shuhey/items/b55c51b555b5120179c4)
- macで `publish` する際は `runtime` をオプションで指定する
  - example : `dotnet publish --runtime osx.10.13-x64`
  - `bin/Debug/netcoreapp2.2/osx.10.13-x64/publish/` にビルドされたものが出力される
    - デフォルトだと名前はプロジェクト名で出力
  - `./<実行バイナリ>` で実行可能

### ver0.3更新

- https://qiita.com/orange634nty/items/5bf8c73612a5d3fbc1db/revisions/5
- https://qiita.com/orange634nty/items/5bf8c73612a5d3fbc1db/revisions/6

ログを ` Microsoft.Extensions.Logging.Console` から `System.Threading.Tasks` に変更  
個人的にはこっちの方がみやすいので嬉しい  
その関連で `RunBatchEngine` から `RunBatchEngineAsync` に変更

### ver0.4更新

ここに関しては特になさそう？

### next

- dotnetコマンド周りの理解 -> 別で行う
- ReadMeもう少し進める

## joの移植

https://qiita.com/gorilla0513/items/e3b0358ffbc0db0a2787

上の記事をみて、自分もMicroBatchFrameworkの勉強用に作ってみたいと思った  
下のやつが移植してみたやつ

- Qiita : https://qiita.com/orange634nty/items/2626fefc5724f3b83bee
- Github : https://github.com/orange634nty/csjo

細かいところは出来てないけど、もう面倒なのでサクッと記事を書いちゃう

MicroBatchFramworkを活かすために、joから仕様を変えている。  

- 配列は`-a`、オブジエクトは`-o`で文字列でしているす
  - 例えば `-a "hoge foo"` のようにしている
  - MicroBatchFrameworkだとパラメータはオプションで受け取る作りになってるので
  - なので`-a`と`-o`は同時に指定できない
- ヘルプは`-h`ではなく`help`で
  - MicroBatchFrameworkで組み込まれているデフォルトの`help`表示機能

汎用的なCLI作成ツールではないなと思った  
それはリポジトリのDescriptionみたらそんな感じな気がした

-> ver0.4からはオプションなしで引数を受けれるようにしたみたい  
その他cliツールぽい作りになったぽい  
後で修正対応する予定
