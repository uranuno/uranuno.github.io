---
title: アニメGIF用の連番キャプチャを撮るエディタ拡張
refs:
  - title: ['uranuno/PlayRecorder', 'GitHub']
    url  : 'https://github.com/uranuno/PlayRecorder'
  - title: ['Unity の画面を Animated GIF に変換して Tumblr にアップする', "keijiro's Gists"]
    url  : 'https://gist.github.com/keijiro/3330732'
  - title: ['QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る', 'Genji App Blog']
    url  : 'http://genjiapp.com/blog/2014/06/04/'
  - title: ['Scripting API: EditorWindow.Update()', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/EditorWindow.Update.html'
  - title: ['Scripting API: Time.captureFramerate', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/Time-captureFramerate.html'
---

![PlayRecorder Result](https://uranuno.github.io/PlayRecorder/out.gif "Cubeくん")

[Unity の画面を Animated GIF に変換して Tumblr にアップする - keijiro's Gists](https://gist.github.com/keijiro/3330732)  
↑これをやりたい！

Tumblr じゃないけど、せっかくブログを始めようと思うので、UnityのキャプチャをアニメGIFで載せたりして、それっぽくしたいです。  
上記に方法が載っているのですが、元になる連番キャプチャをサクッと撮れるように、キャプチャ用スクリプトをつくってみました。

[uranuno/PlayRecorder](https://github.com/uranuno/PlayRecorder)

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
本当は[公式リファレンスのEditorWindow.Update() に載っているサンプルコード](https://docs.unity3d.com/ScriptReference/EditorWindow.Update.html)を参考に[EditorWindow 版を先につくった](https://gist.github.com/uranuno/f558aade1b3ab1f4e3b8)のですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、間隔を細かく調整しようと思うといまいちでした、、
