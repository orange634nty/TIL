uGUI
---

## Drag and Drop

[UnityゲームUI実践ガイド](www.amazon.co.jp/dp/B00U0ZUETW)

こちらを購入したのでちょっとやってみた

ドラッグ＆ドロップを実装するときの処理は大きく分けると2通りあり

1. MonoBehaviour で定義されているイベントを利用する
2. EventTrigger を利用して、別のコンポーネントのメソッドを実行する

### １の場合

アタッチしたGameObjectに関係するもののみに関してはこちらを使った方がいい  
それぞれインターフェイスが用意されているので、使った方がミスが減ります（結構メソッド名が間違えててイベントが正しく発火しないということはよくあるので）

### ２の場合

自身がアタッチしているGameObject以外にイベントを伝えたい時に利用する  
呼び出すにはEventTriggerで呼び出す先のメソッドを指定する必要がある

### サンプル

https://github.com/orange634nty/UnityDragAndDrop
