locust
---

python製の負荷試験ツール  
結構古くから存在している

大まかな使い方はこちらで確認できる。

- [最速でlocustを体験してみた](https://dev.classmethod.jp/articles/20221117_quickly_built_locast_environment/)

### k8sで動かす

以下のhelmのchartが使われているみたいです。

[locust helm](https://github.com/deliveryhero/helm-charts/tree/master/stable/locust)

locustのスクリプトと関連コード類は config map を作成してそれをコンテナ内で mount して使っています。  
使い方は以下の記事に書かれている

[LocustをKubernetesに構築して大規模な負荷テストをする](https://zenn.dev/ry/articles/97a5c50b1ddf16)

関連ファイルのディレクトリがlibと決まってる感じになっているので独自にコピって改造して方がいいかも

manifestを直で書きたい場合は以下のほうが簡素でわかりやすいと思う

[locust を kubernetes にデプロイして負荷テストを実施してみる](https://zenn.dev/empenguin/articles/eda7535aeb0977)
