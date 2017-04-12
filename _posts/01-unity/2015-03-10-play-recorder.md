---
category: unity
title: 連番キャプチャを書き出すエディタ拡張
refs:
  - title: ['uranuno/PlayRecorder', 'GitHub']
    url  : 'https://github.com/uranuno/PlayRecorder'
    class: github
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

[{{ page.refs[1].title[0] }}]({{ page.refs[1].url }}){:target="_blank"}  
↑これをやりたい！

Tumblr じゃないけど、せっかくブログを始めようと思うので、UnityのキャプチャをGIFアニメで載せたりして、それっぽくしたいです。  
上記に方法が載っていますが、元になる連番キャプチャをもっと簡単に撮りたくなったので、エディタ拡張をつくりました。

[{{ page.refs[0].title[0] }}]({{ page.refs[0].url }}){:target="_blank" class="{{ page.refs[0].class }}"}

![PlayRecorder](https://uranuno.github.io/PlayRecorder/playrecorder.png)

<!-- more -->

使い方
-----
.unitypackage をインポートして、PlayRecorder プレハブをScene に置いて使います。  
ゲームの再生中に「Record」ボタンを押すとキャプチャ開始、指定したパスにファイルがぞろぞろ保存されます。

Delay は[ImageMagick](http://www.imagemagick.org/){:target="_blank"} に設定する値と同じもの（1/100秒）を入れられるようにしました。  

### パスの指定
![Edit Path](https://uranuno.github.io/PlayRecorder/save_capture.png)

ファイル名はDateTime をフォーマットするように。  
というわけで連番というのはウソなのですが、ミリ秒まで含めれば重複しないしImage Magick 動くしいいか、と思いました・・・

`EditorUtility.SaveFilePanel` を使っているので、「File Path」の「Edit」ボタンを押すと画像のようにパネルがでます。  
キャプチャ用フォルダをつくりつつパスとして指定する、というのができるのが便利です。  


いまいちなところ
----------------
いちいちScene に置かないと使えないのがちょっと面倒・・・  
[公式リファレンスのEditorWindow.Update() に載っているサンプルコード]({{ page.refs[3].url }}){:target="_blank"}を参考にEditorWindow 版をつくってみたりしたのですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、キャプチャのタイミングが調整しづらかったので、仕方なくそうしています、、
