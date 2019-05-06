dotnet packages
---

使えそうなパッケージについてメモする

## markdown

いくつかあるみたいだけど、markdig使った

https://github.com/lunet-io/markdig

使い方は簡単で

``` csharp
var result = Markdown.ToHtml("This is a text with some *emphasis*");
```

拡張機能を使う場合は

```csharp
var pipeline = new MarkdownPipelineBuilder().UseAdvancedExtensions().Build();
var result = Markdown.ToHtml("This is a text with some *emphasis*", pipeline);
```

でOK
