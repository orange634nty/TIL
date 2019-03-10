bot discord
---

nodeで開発したのでこのライブラリを使用  
[Discord.js](https://github.com/discordjs/discord.js/)

導入方法：[Discord.jsで簡単にbotを作成する【基礎編】](https://qiita.com/cryptocoin_harumaki/items/5d8c503e02093eca1f9b)

このbotでいくつかのアプリと連隊したいと考えていた

- trello
- kibela

## trello連帯

外部ライブラリを使わず、httpリクエストで実装  
トークン発行：[Node.jsでTrelloとSlackとTwitterを連携させてタスク管理をちょっと良い感じにする](https://qiita.com/nabeliwo/items/d5c6e22be0fc42919d52)

APIは本家の奴を直接参照  
APIドキュメント：[TRELLO REST API](https://developers.trello.com/v1.0/reference#introduction)

httpリクエストは axios をなぜか使わず http モジュールを使用  
参考：[Node.jsの標準モジュール(https)でAPIを叩く(GETのみ)](https://qiita.com/r-yanyo/items/3ef153dac12e69a2c46c)

trelloの項目が変更した時の web hook 通知も実装

導入方法はこれを参考に  
[Trello Webhook × GoogleAppsScript の連携してカンバンの分析を楽にして見る](https://qiita.com/yokozawa0701/items/8b98fd69ea401bf260e0) 
[Webhook APIを使ってTrelloとchatworkを連携する](https://qiita.com/Andysumi/items/462964bd8249beb067e4)  
[Webhooks](https://developers.trello.com/page/webhooks)

開発者用のAPI発行後それを使って、postでwebhook先のurlとボードを連帯  
連帯外すことも可能  
このAPIの詳細は本家のAPIドキュメントに書いてあるので、頑張って読む

ローカルで試すために ngrok を使用  
[ローカル開発環境でZenHubのWebhookを受け取る方法を試す](https://qiita.com/kentaro_m/items/90e577d36be7a271fa78)
[Node.jsでPayPalの商品購入の通知(Webhook)を受け取る](https://qiita.com/n0bisuke/items/8484777c3b41448eddc3)

どう言ったリクエストがくるかですが…どうやったか覚えてない…
たぶん、投げてくるリクエストの中身読んで頑張って感じ取ったんだろうと思う




