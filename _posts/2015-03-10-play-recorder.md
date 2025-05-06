---
category: Unity
title: 連番キャプチャを書き出すエディタ拡張
description: 連番キャプチャをもっと簡単に撮りたくなったので、エディタ拡張をつくりました。
---

> [!WARNING]  
> Unity2018 くらいからは[Unity Recorder][UnityRecorderPackage] という公式package があります ‼️ 

[UnityRecorderPackage]: https://docs.unity3d.com/ja/Packages/com.unity.recorder@2.6/manual/index.html

<figure class="ar-4-3 top">
  <img src="https://uranuno.github.io/PlayRecorder/out.gif" alt="回るCubeくんのアニメGIF" width="400" />
  <figcaption>Cubeくん</figcaption>
</figure>

[Unity の画面を Animated GIF に変換して Tumblr にアップする](https://gist.github.com/keijiro/3330732)  
↑これをやりたい！

Tumblr じゃないけど、せっかくブログを始めようと思うので、UnityのキャプチャをGIFアニメで載せたりして、それっぽくしたいです。  
上記に方法が載っていますが、元になる連番キャプチャをもっと簡単に撮りたくなったので、エディタ拡張をつくりました。

**uranuno/PlayRecorder**  
<https://github.com/uranuno/PlayRecorder>

<figure>
  <img src="https://uranuno.github.io/PlayRecorder/playrecorder.png" alt="Unity Inspector のスクリーンショット" width="800" />
  <figcaption>エディタはこんなかんじ</figcaption>
</figure>


## 使い方

.unitypackage をインポートして、PlayRecorder プレハブをScene に置いて使います。  
ゲームの再生中に「Record」ボタンを押すとキャプチャ開始、指定したパスにファイルがぞろぞろ保存されます。

Delay は[ImageMagick](https://imagemagick.org/) に設定する値と同じもの（1/100秒）を入れられるようにしました。  

### パスの指定

<figure>
  <img src="https://uranuno.github.io/PlayRecorder/save_capture.png" alt="Mac のFinder が開いて保存場所を指定しているスクリーンショット" width="800" />
  <figcaption>パス指定画面</figcaption>
</figure>

ファイル名はDateTime をフォーマットするように。  
というわけで連番というのはウソなのですが、ミリ秒まで含めれば重複しないしImage Magick 動くしいいか、と思いました・・・

`EditorUtility.SaveFilePanel` を使っているので、「File Path」の「Edit」ボタンを押すと画像のようにパネルがでます。  
キャプチャ用フォルダをつくりつつパスとして指定する、というのができるのが便利です。  


## いまいちなところ

いちいちScene に置かないと使えないのがちょっと面倒・・・  
[公式リファレンスのEditorWindow.Update() に載っているサンプルコード][EditorWindowUpdateRef]を参考にEditorWindow 版をつくってみたりしたのですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、キャプチャのタイミングが調整しづらかったので、仕方なくそうしています、、

[EditorWindowUpdateRef]: https://docs.unity3d.com/ScriptReference/EditorWindow.Update.html


## 他参考

- [QuickTime PlayerでスクリーンキャプチャしたMOVからベターなアニメーションGIFを作る — Genji App Blog](https://genjiapp.com/blog/2014/06/04/generating-better-animated-gif-from-mov-recorded-by-quicktime-player.html)
- [Unity - Scripting API: Time.captureFramerate](https://docs.unity3d.com/ScriptReference/Time-captureFramerate.html)
