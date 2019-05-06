Directory
---

## 特定のディレクトリ以下のファイルを全て取得する（サブフォルダ含む）

[Directory.EnumerateFiles](https://docs.microsoft.com/ja-jp/dotnet/api/system.io.directory.enumeratefiles?view=netcore-2.2)

を使用します。

```csharp
var markDownFiles = Directory.EnumerateFiles(sourceDirectory, "*.md", SearchOption.AllDirectories);
```

検索するパターンは `*` or `?` でのみ表現できます。  
正規表現は使えません。

また、戻り値は `IEnumerable<String>` なので注意。
