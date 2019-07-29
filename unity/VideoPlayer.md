VideoPlayer tips
---

## 動画を再生する

[Unityで動画素材を表示する方法](https://qiita.com/squall22446688/items/256a1c7468430c681844)

## 動画の終了にメソッドを呼び出す

参考：https://stackoverflow.com/questions/44696030/detect-when-videoplayer-has-finished-playing

ただ、このまま実装すると動画再生枚にコルーチンが走ってしまう場合があるので、しばらく待ってから再生判定を行う方がいい

```csharp
    private void StartVideo(int videoId)
    {
        videoPlayer.Play();
        StartCoroutine(CheckVideoPlayEnd());
    }

    private IEnumerator CheckVideoPlayEnd()
    {
        // 直ぐにコルーチンをはじめると動画再生始まる前に再生がスタートするので、1秒待つ
        yield return new WaitForSeconds(WAIT_TIME_FOR_CHECK);
        while (videoPlayer.isPlaying)
        {
            yield return null;
        }
        // 再生後処理
    }
```
