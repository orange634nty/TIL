RazorEngine RazorLight
---

ASP.NET MVC3 のに追加されたビューのレンダリングエンジンを切り出したやつ。  

Github : https://github.com/Antaris/RazorEngine

後で試す

参考 : https://blog.shibayan.jp/entry/20130201/1359694543

---

これを使おうと考えていたが、実は .Net Framework 依存らしくて、 .Net Core では使えないみたい……

.Net Core 向けの [RazorLight](https://github.com/toddams/RazorLight) というのがあるので、こちらを使うので良さそう

RazorLight を動かす際に以下のtagをcsprojに追加する必要があります。

```xml

<PropertyGroup>
  ...
  <PreserveCompilationContext>true</PreserveCompilationContext>
  <MvcRazorCompileOnPublish>false</MvcRazorCompileOnPublish>
</PropertyGroup>
```

参考

- https://github.com/toddams/RazorLight#im-getting-cant-load-metadata-reference-from-the-entry-assembly-exception
- https://github.com/toddams/RazorLight/issues/127
- https://docs.microsoft.com/ja-jp/aspnet/core/mvc/views/view-compilation?view=aspnetcore-2.2
