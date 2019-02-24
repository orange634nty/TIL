.NET cli
---

## dotnet publish

mac向けにビルドする方法

- https://qiita.com/yaegaki/items/bdf529f07552d72bc6e5
- https://docs.microsoft.com/ja-jp/dotnet/core/tools/dotnet-publish?tabs=netcore21

mac用のランタイムをしてビルド

```
$ dotnet publish --runtime osx.10.13-x64
```

みたいにしてビルド  
`./bin/Debug/netcoreapp2.2/osx.10.13-x64/publish/` にビルドされたものが出力されます
そのバイナリは

```
$ <hogehoge>
```

で実行出来ます

