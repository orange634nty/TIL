SE Linux
---

あの適当に無効にしていたやつだけど、ダメらしい  
ローカルのVMは割と適当に設定無効にしてた記憶

https://blog.fenrir-inc.com/jp/2016/09/selinux.html

ちょっとわかった

これ読むといいらしい  
https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide/

基本的に、SE Linux を有効にしなければいけない場合は実行ユーザーが root だったりする  
例えば nginx を動かす場合は root ではなく、それ用のユーザーを作成してそれで実行するべきである（セキュリティ的な観点から）  
root でやると 100% SE Linux に怒られるからだめ
