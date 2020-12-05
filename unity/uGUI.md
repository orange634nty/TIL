uGUI
---

## Drag and Drop

[UnityゲームUI実践ガイド](www.amazon.co.jp/dp/B00U0ZUETW)

こちらを購入したのでちょっとやってみた

ドラッグ＆ドロップを実装するときの処理は大きく分けると2通りあり

1. MonoBehaviour で定義されているイベントを利用する
2. EventTrigger を利用して、別のコンポーネントのメソッドを実行する

どちらの場合でもイベントが発火したときは `EventSystems.PointerEventData` を受け取ることになります。  
https://docs.unity3d.com/ja/2018.3/ScriptReference/EventSystems.PointerEventData.html

(EventTriggerの時は `EventSystem.BaseEventData` で来るので、キャストする必要があります)  
https://docs.unity3d.com/ja/2018.3/ScriptReference/EventSystems.BaseEventData.html

今回の場合はドラッグ時のPointerの移動差分の取得とドラッグしているGameObjectを取得するのに使いました。

- [delta](https://docs.unity3d.com/ja/2018.3/ScriptReference/EventSystems.PointerEventData-delta.html)
- [pointerDrag](https://docs.unity3d.com/ja/2018.3/ScriptReference/EventSystems.PointerEventData-pointerDrag.html)

### １の場合

アタッチしたGameObjectに関係するもののみに関してはこちらを使った方がいい  
それぞれインターフェイスが用意されているので、使った方がミスが減ります（結構メソッド名が間違えててイベントが正しく発火しないということはよくあるので）

### ２の場合

自身がアタッチしているGameObject以外にイベントを伝えたい時に利用する  
呼び出すにはEventTriggerで呼び出す先のメソッドを指定する必要がある

### サンプル

https://github.com/orange634nty/UnityDragAndDrop

## タップした位置にuGUI表示

http://ghoul-life.hatenablog.com/entry/2018/11/13/000955

Staticな位置はUGUIでは使いやすいが、こういう動的な場合はどうするかわからなかったのでメモ

## Canvas内でImageをInstantiateするときの注意

https://qiita.com/tibe/items/5e1ae977c31cdbec1e60

```csharp
prefab.transform.SetParent(canvas.transform, false);
```

`false` にしないとダメ

## アスペクト比を固定にする

http://tsubakit1.hateblo.jp/entry/2014/12/11/223427

カメラのアス比はこんな感じで固定できるらしい: https://meideru.com/archives/556

## uGUIでPanelとかのタッチ判定を後ろに流す

https://www.stmn.tech/entry/2018/06/17/152357

RaycastTarget を有効・無効に切り替えることで利用可能

## uGUIのScrollView

https://q7z.hatenablog.com/entry/2016/12/03/000027

上の記事は色々細かいところも書いてるので役に立つ
