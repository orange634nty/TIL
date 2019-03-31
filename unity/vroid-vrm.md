VRoid・VRM
---

VRoid: https://studio.vroid.com/

VRM: https://dwango.github.io/vrm/

## Vroidで作ったキャラをUniVRMを使ってUnityに表示して躍らせる

完成したらこんな感じ  
https://twitter.com/orange634nty/status/1112285426293706754  
<画像は後で貼る>

主にこれを参考

[「VRoid Studio」で作った3Dモデルを「Unity」で踊らせてみよう](https://3owebcreate.com/web/design/vroid_studio_dance)

モデルはこれを使います

https://twitter.com/orange634nty/status/1112228133745258496  
<画像は後で貼る>

記事のやり方といくつか変えていて

- 色々なエラーが出るのでここを参考に消す
  - ["error CS0234: The type or namespace name 'Policy' does not exist in the namespace 'System.Security'" エラーが発生する (Unityプログラミング)](https://www.ipentec.com/document/unity-error-cs0234-the-type-or-namespace-name-policy-does-not-exist-in-namespace-system-security)
  - [unityについて質問です。](https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q12204854092)
- 記事だとバックダンサーだけど中心で踊るように変更
  - MainシーンのStageDirectorプレハブのインスペクターの、 `[Stage Director(Script)] -> [Prefabs On Timeline] -> [Element 0]` にVRMで読み込んだモデルを指定しまう
  - シーンを再生すると中央に立っています
  - 自分の作ったモデルだと身長が足りずカメラに映らないので、カメラに位置を調整します
- モデルのライトを周りとなじむように変更

疑問

`AIUEO` というコンポーネントがなかった。これがなかったので歌に合わせて表情が変えられなかった…

