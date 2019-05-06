Array
---

Listは別にメモをする

## 配列に値が含まれているか確認する

List には [Contais](https://docs.microsoft.com/ja-jp/dotnet/api/system.collections.generic.list-1.contains?view=netcore-2.2) があるが、ArrayにはContaisはありません。  
なので Linq の [Enumerable.Contains](https://docs.microsoft.com/ja-jp/dotnet/api/system.linq.enumerable.contains?view=netcore-2.2) を使います

```csharp
string[] fruits = {"apple", "banana", "orange"};
      
if(friends.Contains("tomato")) {
    Console.WriteLine("exist!");
} else {
    Console.WriteLine("not exist...");
}
```
