---
category: Unity
title: 連番キャプチャを書き出すエディタ拡張
---

{: .note}
追記: Unity2018 くらいからは  
[Unity Recorder][UnityRecorderPackage] という公式package があります！

![Cubeくん][Cube-kun]{:standalone width="400" .ar-4-3 .top}

[Unity の画面を Animated GIF に変換して Tumblr にアップする][UnityGIFTumblr]  
↑これをやりたい！

Tumblr じゃないけど、せっかくブログを始めようと思うので、UnityのキャプチャをGIFアニメで載せたりして、それっぽくしたいです。  
上記に方法が載っていますが、元になる連番キャプチャをもっと簡単に撮りたくなったので、エディタ拡張をつくりました。

[**uranuno/PlayRecorder**][PlayRecorder]

![エディタはこんなかんじ][PlayRecorderView]{:standalone width="800" height="400"}

使い方
-----
.unitypackage をインポートして、PlayRecorder プレハブをScene に置いて使います。  
ゲームの再生中に「Record」ボタンを押すとキャプチャ開始、指定したパスにファイルがぞろぞろ保存されます。

Delay は[ImageMagick] に設定する値と同じもの（1/100秒）を入れられるようにしました。  

### パスの指定
![パス指定画面][EditPathView]{:standalone width="800" height="400"}

ファイル名はDateTime をフォーマットするように。  
というわけで連番というのはウソなのですが、ミリ秒まで含めれば重複しないしImage Magick 動くしいいか、と思いました・・・

`EditorUtility.SaveFilePanel` を使っているので、「File Path」の「Edit」ボタンを押すと画像のようにパネルがでます。  
キャプチャ用フォルダをつくりつつパスとして指定する、というのができるのが便利です。  


いまいちなところ
----------------
いちいちScene に置かないと使えないのがちょっと面倒・・・  
[公式リファレンスのEditorWindow.Update() に載っているサンプルコード][EditorWindowUpdateRef]を参考にEditorWindow 版をつくってみたりしたのですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、キャプチャのタイミングが調整しづらかったので、仕方なくそうしています、、

他参考
------
- [QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る — Genji App Blog][BetterAnimatedGIF]
- [Unity - Scripting API: Time.captureFramerate][CaptureFramerateRef]


[Cube-kun]: https://uranuno.github.io/PlayRecorder/out.gif

[UnityGIFTumblr]: https://gist.github.com/keijiro/3330732

[PlayRecorder]: https://github.com/uranuno/PlayRecorder
[PlayRecorderView]: https://uranuno.github.io/PlayRecorder/playrecorder.png

[ImageMagick]: https://imagemagick.org/

[EditPathView]: https://uranuno.github.io/PlayRecorder/save_capture.png

[EditorWindowUpdateRef]: https://docs.unity3d.com/ScriptReference/EditorWindow.Update.html
[BetterAnimatedGIF]: https://genjiapp.com/blog/2014/06/04/generating-better-animated-gif-from-mov-recorded-by-quicktime-player.html
[CaptureFramerateRef]: https://docs.unity3d.com/ScriptReference/Time-captureFramerate.html

[UnityRecorderPackage]: https://docs.unity3d.com/ja/Packages/com.unity.recorder@2.6/manual/index.html
