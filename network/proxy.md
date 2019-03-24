proxy
---

## mac で proxy を行う方法

以前までは [Macでproxy.pacを設定したいとき](https://qiita.com/siukaido/items/340f46e9bbc86887d218) を参考に pac ファイルを使ってproxyを使っていました。
ただ、最近突然使えなくなりました。

調べたところ、

https://developer.apple.com/documentation/macos_release_notes/macos_mojave_10_14_release_notes?language=objc

```
Deprecations
The ftp:// and file:// URL schemes for Proxy Automatic Configuration (PAC) are deprecated. HTTP and HTTPS are the only supported URL schemes for PAC. This affects all PAC configurations including, but not limited to, configurations set via Settings, System Preferences, profiles, and NSURLSession APIs such as connectionProxyDictionary, and CFNetworkExecuteProxyAutoConfigurationURL. (37811761)
```

どうやら使えなくなったらしい

なので、今はchromeの拡張機能を使ってproxyを使っています。

[Chrome ウェブストア Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif/related)

設定方法とかはここを参考に

[Chromeで特定サイトのみプロキシ経由でアクセスする拡張機能Proxy SwitchyOmega](https://qiita.com/zakisanf05/items/acaf0b27bdf614a8cf44)

この拡張機能はpacファイルも使えるので、以前使っていたpacファイルの中身をコピペして設定しています。
