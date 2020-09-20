mac tips
---

## ターミナルで標準出力をコピペする

```
$ echo "hello world" | pbcopy
```

参考：[ターミナルで標準出力をクリップボードにコピーする](https://qiita.com/sasaplus1/items/137a70e8f51f97a6636f)

## macでのデーモン化

redisやmemchachedはmacではデーモン化しておくと便利  
redisはやり方はこの通り

[homebrewでインストールしたredisを自動起動](https://qiita.com/marqs/items/05cec2b1a305b50ee7b2)

簡単な説明は以下を参照

[Macのlaunchctlでサービスの自動起動をさせたくない時のためのメモ](https://qiita.com/ono_matope/items/e437a35c3921ad35d109)

## brew cask

app をインストールできる  
普通に brew をインストールしたら入ってる

## macでmovからmp4へ変換する 

アプリとかあんまり入れなたくないので方法が探したけど、`ffmpeg`のが一番良さそう。  
`ffmpeg`はgifの変換出来るみたいなので色々使えそう。  
ちなみに、この方法は特に mac 限定ではない。

```
$ ffmpeg -i movie.mov  movie.mp4
```
# 参考
- [twitterに動画が投稿できない場合の対処法 〜 フリーソフトを使わずに動画を .mp4に変換する方法、.mov形式は使えない](https://www.what-a-day.net/entry/movie-convert-mp4)
- [macでffmpegを導入してmovファイルをgifファイルへ変換するところまで](https://qiita.com/Ryosuke-Hujisawa/items/6a1c47d31ac299dc1c46)
