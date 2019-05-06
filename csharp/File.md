File
---

## ファイルのコピー

[File.Copy](https://docs.microsoft.com/ja-jp/dotnet/api/system.io.file.copy?view=netcore-2.2) を使えばOK

```csharp
File.Copy("コピー元パス", "コピー先パス");
```

## テキストファイル読み込み

ファイルのテキストが大きくない場合は [File.ReadAllText](https://docs.microsoft.com/ja-jp/dotnet/api/system.io.file.readalltext?view=netcore-2.2) を使えばOK

`StreamReader` 使って読み込んだ方がいいかも  
`ReadAllText` はファイルを開いて全文字を読み込んでからファイルを閉じるので、ファイルが大きい場合時間がかかるし、一度に読み込めないかもしれない。

[方法: テキスト ファイルを一度に 1 行読み込む (Visual C#)](https://docs.microsoft.com/ja-jp/dotnet/csharp/programming-guide/file-system/how-to-read-a-text-file-one-line-at-a-time)

