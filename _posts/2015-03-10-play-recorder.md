---
title: Unity のゲーム画面からAnimated GIF をつくるための連番キャプチャをサクッと撮る
tags: [unity]
---

![PlayRecorder Result](https://uranuno.github.io/PlayRecorder/out.gif "Cubeくん")

[Unity の画面を Animated GIF に変換して Tumblr にアップする - keijiro's Gists][UnityAnimeGif]  
↑これをやりたい！

Tumblr じゃないけど、せっかくブログを始めようと思うので、UnityのキャプチャをアニメGIFで載せたりして、それっぽくしたいです。  
上記に方法が載っているのですが、元になる連番キャプチャをサクッと撮れるように、キャプチャ用スクリプトをつくってみました。

[uranuno/PlayRecorder :octocat:](https://github.com/uranuno/PlayRecorder)

![PlayRecorder](https://uranuno.github.io/PlayRecorder/playrecorder.png)

<!-- more -->

使い方
-----

.unitypackage をインポートして、PlayRecorder プレハブをScene に置いて使います。  
ゲームの再生中に「Record」ボタンを押すとキャプチャ開始、指定したパスにファイルがぞろぞろ保存されます。

Delay は[ImageMagick](http://www.imagemagick.org/) に設定する値と同じもの（1/100秒）を入れられるようにしました。  

### パスの指定
![Edit Path](https://uranuno.github.io/PlayRecorder/save_capture.png)

ファイル名はDateTime をフォーマットするように。  
というわけで連番というのはウソなのですが、ミリ秒まで含めれば重複しないしImage Magick 動くしいいか、と思いました・・・

[EditorUtility.SaveFilePanel](http://docs.unity3d.com/ScriptReference/EditorUtility.SaveFilePanel.html) を使っているので、「File Path」の「Edit」ボタンを押すと画像のようにパネルがでます。  
キャプチャ用フォルダをつくりつつパスとして指定する、というのができるので便利です。  


ちょっと面倒なところ
--------------------
いちいちScene に置かないと使えないのがちょっと面倒・・・  
本当は[公式リファレンスのEditorWindow.Update() に載っているサンプルコード][UnityAPIEditorWindowUpdate]を参考に[EditorWindow 版を先につくった](https://gist.github.com/uranuno/f558aade1b3ab1f4e3b8)のですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、間隔を細かく調整しようと思うといまいちでした、、

2015.07.15 追記
---------------
[Time.captureFramerate][UnityAPIcaptureFramerate]という便利なものを知ったので、それをつかうようにしました。

参考
-----
- [Unity の画面を Animated GIF に変換して Tumblr にアップする - keijiro's Gists][UnityAnimeGif]
- [QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る - Genji App Blog][QTAnimeGif]
- [Scripting API: EditorWindow.Update() - Unity][UnityAPIEditorWindowUpdate]
- [Scripting API: Time.captureFramerate - Unity][UnityAPIcaptureFramerate]

[UnityAnimeGif]: https://gist.github.com/keijiro/3330732
[QTAnimeGif]: http://genjiapp.com/blog/2014/06/04/generating-better-animated-gif-from-mov-recorded-by-quicktime-player.html
[UnityAPIEditorWindowUpdate]: http://docs.unity3d.com/ScriptReference/EditorWindow.Update.html
[UnityAPIcaptureFramerate]: http://docs.unity3d.com/ScriptReference/Time-captureFramerate.html