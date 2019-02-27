scp
---

多段scp

踏み台を使う場合のscp  
一番手っ取り早いのは、`.ssh/config`に多段sshが出来るように設定をする

その後

```
$ scp -r -P <port> <転送したいフォルダへのパス> <sshの送り先>:<転送先のディレクトリ>
```

で作成出来ます。

オプションは

- `-r`：再帰的
- `-P`：ポート番号

です。

#### 参考

- https://qiita.com/S-T/items/18af2bfcc4e5a72202da
- https://qiita.com/tommyfms2/items/7d7732c0b681b215d461
