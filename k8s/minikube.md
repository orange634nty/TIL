minikube
---

ローカルでk8s用の環境  
コマンド一発で作成・削除ができるので検証としても使える

[minikube 公式](https://minikube.sigs.k8s.io/docs/)

以下のサイトを参考にしました。

[Docker Desktop の代わりに Minikube を使ってみる](https://blog.1q77.com/2021/09/replace-docker-desktop-with-minikube/)

minikube 上でビルドしたイメージを使いたい場合はバックエンドを docker にして minikube 環境でビルドする必要があります。  
参考 : [Kubernetes入門 - 自作のDockerイメージをminikubeで動かす方法](https://tech.andpad.co.jp/entry/2021/02/18/170000)

注意としては docker for desktop などを使ってるときは minikube の県境に切り替える必要があります。  
やりたかは最初の資料に書いてあるのでそちら参照。
