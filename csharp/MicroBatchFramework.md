# MicroBatchFramework

## 使ってみた

- Qiita : https://qiita.com/orange634nty/items/5bf8c73612a5d3fbc1db
- Github : https://github.com/orange634nty/micro-batch-test

### 学び

- `dotnet add package` でパッケージを入れても自動で依存解決してくれないみたい
  - その時は手動で追加した
- cotnet 2.2 だと、c# のバージョンはデフォルトだと 7.0 なので、自分で指定する必要があり
  - `.csproj` ファイルで `<LangVersion>7.3</LangVersion>` を追加
  - 参考 : [.Net CoreプロジェクトでC#のバージョンを変更する方法](https://qiita.com/shuhey/items/b55c51b555b5120179c4)
- macで `publish` する際は `runtime` をオプションで指定する
  - example : `dotnet publish --runtime osx.10.13-x64`
  - `bin/Debug/netcoreapp2.2/osx.10.13-x64/publish/` にビルドされたものが出力される
    - デフォルトだと名前はプロジェクト名で出力
  - `./<実行バイナリ>` で実行可能

### next

- dotnetコマンド周りの理解 -> 別で行う
- ReadMeもう少し進める
