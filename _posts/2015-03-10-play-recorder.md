---
layout: post
title: Unity のゲーム画面を連写でキャプチャする
tag: [unity3d]
---

![PlayRecorder](http://uranuno.github.io/PlayRecorder/playrecorder.png)

[Github - PlayRecorder](https://github.com/uranuno/PlayRecorder)

[Unity の画面を Animated GIF に変換して Tumblr にアップする][UnityAnimeGif]  
↑これをやりたい！と思ったときに、元の連番キャプチャをサクッと撮りたいと思い、キャプチャ用クラス＆エディタスクリプトを書きました。

<!-- more -->

Delay は[ImageMagick](http://www.imagemagick.org/) に設定する値と同じもの（ms）を入れられるようにしました。  
フレーム落ち対策で、フレームカウントに換算して撮るようにしています。


パスの指定
----------
![PlayRecorder](http://uranuno.github.io/PlayRecorder/save_capture.png)

ファイル名はDateTime をフォーマットするように。  
`EditorUtility.SaveFilePanel` を使っているので、「Saved Path」の「Edit」ボタンを押すと画像のようにパネルがでます。  
キャプチャ用フォルダをつくりつつパスとして指定する、というのもできます。  
連番をつける機能はサボって入れてませんが、ミリ秒まで含めれば重複しないしいいか、と思いました。


使い方
-----
PlayRecorder プレハブをシーンに置いて使います。  
いちいち置かないといけないのがちょっと面倒。  
本当は[公式リファレンス][UnityAPIEditorWindowUpdate]を参考に[EditorWindow 版を先につくった](https://gist.github.com/uranuno/f558aade1b3ab1f4e3b8)のですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、間隔を細かく調整しようと思うと、いまいちでした…


参考
----------
- [Unity の画面を Animated GIF に変換して Tumblr にアップする][UnityAnimeGif]
- [QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る][QTAnimeGif]
- [Unity - Scripting API: EditorWindow.Update()][UnityAPIEditorWindowUpdate]

[UnityAnimeGif]: https://gist.github.com/keijiro/3330732
[QTAnimeGif]: http://genjiapp.com/blog/2014/06/04/generating-better-animated-gif-from-mov-recorded-by-quicktime-player.html
[UnityAPIEditorWindowUpdate]: http://docs.unity3d.com/ScriptReference/EditorWindow.Update.html