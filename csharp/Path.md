Path
---

## フルパスを取得する

[Path.GetFullPath](https://docs.microsoft.com/ja-jp/dotnet/api/system.io.path.getfullpath?view=netcore-2.2) を使えば一発解決

```csharp
Path.GetFullPath(path);
```

## フルパスを相対パスに変換する
 
これは一つのメソッドで簡単には出来ません。  
stringのパスをUriに変換してから、[Uri.MakeRelativeUri](https://docs.microsoft.com/ja-jp/dotnet/api/system.uri.makerelativeuri?view=netcore-2.2)メソッドで相対Uriを取得して文字列に変換する。

```csharp
Uri filePathUri = new Uri(filePath);
Uri basePathUri = new Uri(basePath);
Console.Writeline(basePathUri.MakeRelativeUri(filePathUri).ToString());
```
