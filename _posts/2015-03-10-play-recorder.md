---
layout: post
---

![PlayRecorder](http://uranuno.github.io/PlayRecorder/playrecorder.png)

[https://github.com/uranuno/PlayRecorder](https://github.com/uranuno/PlayRecorder)

Unity の画面キャプチャを撮るクラスをつくりました。  
1枚撮るのもよし、delay を指定して連写もできます。  
連写は再生中のみ動きます。

撮る時にフレームレート落ちますが、フレームカウントに換算しているのでフレーム落ちしないはず・・・  
ファイル名は連番付けるのが面倒だったので、DateTimeのミリ秒部分まで含めて重複しないようにしています。（フォーマットは変えられます）  

ImageMagick をつかって、キャプチャでGifアニメをつくりたいときに便利。

- - -

## 参考
- [Unity の画面を Animated GIF に変換して Tumblr にアップする](https://gist.github.com/keijiro/3330732)
- [QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る](http://genjiapp.com/blog/2014/06/04/generating-better-animated-gif-from-mov-recorded-by-quicktime-player.html)
- [Unity - Scripting API: EditorWindow.Update()](http://docs.unity3d.com/ScriptReference/EditorWindow.Update.html)
