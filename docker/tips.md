tips for docker
---

## Spectre脆弱性対策の関係で docker で ruby や python が遅くなる場合がある

参考: https://mametter.hatenablog.com/entry/2020/05/23/032650

遅いからと言って off にするのは懸命な判断ではないので、しないこと  
試してないので不明だが言うほど遅くはならないらしい

## WSL2で `docker-compose` がなぜか `docker-compose-v1` を呼びだそうとしてエラーになる

Windows の Docker for Desktop を使っています。

```
$ docker-compose --version
exec: "docker-compose-v1": executable file not found in $PATH
```

いくら探しても `docker-compose-v1` はみつからない

### 解決方法

そもそも作業環境のWSLとデフォルトのwslが異なっていたため、Docker for Desktop の WSLのバックエンドの向き先が異なっていただけみたいでした。  
参考: https://ginpen.com/2020/11/24/wsl-2-cannot-connect-to-the-docker-daemon/

