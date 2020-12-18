ansible tips
---

# ansibleでこれはどうするの？（逆引き）

## git

標準のgitモジュールを使う

http://qiita.com/seizans/items/f5f052aec1592c47767f
http://docs.ansible.com/ansible/git_module.html

## ディレクトリ作成

fileモジュールを使う

https://stackoverflow.com/questions/22844905/how-to-create-a-directory-using-ansible/27654582
http://docs.ansible.com/ansible/file_module.html

## ファイルのmode変更

同じくfileモジュール使う

http://docs.ansible.com/ansible/file_module.html

なぜかうまくいかない時も。。。

### ファイルモードに関して

４桁目全然わかってなかった

- https://blog.fenrir-inc.com/jp/2012/02/file_permission.html
- http://kazmax.zpp.jp/linux_beginner/setgroupid.html

## visudo

linefile使う
下の例でやればOK

https://blog.adachin.me/archives/5475

## ansibleでのcomposerについて

デフォルトでは --no-dev で require-dev に入っているものは省かれるので、no_dev: no（否定を否定）にする必要がある。
