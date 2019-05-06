Path
---

## 絶対パスを取得する

[Path.GetFullPath](https://docs.microsoft.com/ja-jp/dotnet/api/system.io.path.getfullpath?view=netcore-2.2) を使えば一発解決

```csharp
Path.GetFullPath(path);
```

`path` は相対で指定したものを使う

## 絶対パスを相対パスに変換する
 
これは一つのメソッドで簡単には出来ません。  
stringのパスをUriに変換してから、[Uri.MakeRelativeUri](https://docs.microsoft.com/ja-jp/dotnet/api/system.uri.makerelativeuri?view=netcore-2.2)メソッドで相対Uriを取得して文字列に変換する。

```csharp
Uri filePathUri = new Uri(filePath);
Uri basePathUri = new Uri(basePath);
Console.Writeline(basePathUri.MakeRelativeUri(filePathUri).ToString());
```

## 相対パスか絶対パスか判定する

[Path.IsPathRooted](https://docs.microsoft.com/ja-jp/dotnet/api/system.io.path.ispathrooted?view=netcore-2.2) で一発

文字列から判定するのはOS依存操作なのでよくない。  
例えば linux なら先頭が `/` で絶対パスか判定可能だが、Windowsの場合は `C:\\` や `D:\\` になるので正常に動作しない。  

## Path色々

https://dobon.net/vb/dotnet/file/pathclass.html

```csharp
string path = "/path/to/file/index.html";

//ディレクトリ名の取得
Console.WriteLine(Path.GetDirectoryName(path)); // => /path/to/file

//拡張子の取得
Console.WriteLine(Path.GetExtension(path)); // => .html

//ファイル名の取得
Console.WriteLine(Path.GetFileName(path));  // => index.html

//ファイル名（拡張子なし）の取得
Console.WriteLine(Path.GetFileNameWithoutExtension(path)); // => index

//ルートディレクトリ名の取得
Console.WriteLine(Path.GetPathRoot(path)); // => /
```
