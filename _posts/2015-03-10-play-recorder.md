---
layout: post
title: Unity のスクリーンショットを連写する
tag: [unity]
---

![PlayRecorder](http://uranuno.github.io/PlayRecorder/playrecorder.png)

[https://github.com/uranuno/PlayRecorder](https://github.com/uranuno/PlayRecorder)

Unity のスクリーンショットを撮るクラスをつくりました。  
1枚でも撮れますが、メインは再生しながらの連写機能です。  

<!-- more -->

連写したキャプチャはImageMagick を使って、Gifアニメにする想定です。  
Delay はImageMagick に設定する値と同じものを入れればOK。  
フレーム落ち対策で、フレームカウントに換算して撮るようにしています。

ファイル名はDateTime をフォーマットするようになっています。  
連番をつける機能はサボって入れてませんが、ミリ秒まで含めれば重複しないしいいか、と思いました。

PlayRecorder プレハブをシーンに置いて使います。  
いちいち置かないといけないのがちょっと面倒。  
本当は[EditorWindow 版を先につくった](https://gist.github.com/uranuno/f558aade1b3ab1f4e3b8)のですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、いまいちでした…

- - -

## 参考
- [Unity の画面を Animated GIF に変換して Tumblr にアップする](https://gist.github.com/keijiro/3330732)
- [QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る](http://genjiapp.com/blog/2014/06/04/generating-better-animated-gif-from-mov-recorded-by-quicktime-player.html)
- [Unity - Scripting API: EditorWindow.Update()](http://docs.unity3d.com/ScriptReference/EditorWindow.Update.html)
