Tap Effect
---

Unityにはデフォルトスタンダードのようなタップエフェクトの作り方はなく、いくつかの方法が存在する。

- パーティクルを使う方法
  - http://tsubakit1.hateblo.jp/entry/2016/04/28/023104
- シェーダーで作る方法
  - https://qiita.com/katsuma99/items/9eb6b2a338fb7303c9b8

どれでもいいが自分に必要なものを使うのがいいです

### 注意

実際に遭遇して困ったが、タップエフェクトをuGUIの上で行う場合、Cnavasの設定をOverlayにしていた為にuGUIの上のエフェクトが描画できなかった  
CameraかWorldScaleにする必要がある
