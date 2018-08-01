---
category: unity
title: 連番キャプチャを書き出すエディタ拡張
source:
  title: ['uranuno/PlayRecorder', 'GitHub']
  url  : 'https://github.com/uranuno/PlayRecorder'
refs:
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

{% assign ref=page.refs[0] %}
{% include link.html param=ref blank=1 %}  
↑これをやりたい！

Tumblr じゃないけど、せっかくブログを始めようと思うので、UnityのキャプチャをGIFアニメで載せたりして、それっぽくしたいです。  
上記に方法が載っていますが、元になる連番キャプチャをもっと簡単に撮りたくなったので、エディタ拡張をつくりました。

{% assign source=page.source %}{% include link.html param=source blank=1 %}

![PlayRecorder](https://uranuno.github.io/PlayRecorder/playrecorder.png)

<!-- more -->

使い方
-----
.unitypackage をインポートして、PlayRecorder プレハブをScene に置いて使います。  
ゲームの再生中に「Record」ボタンを押すとキャプチャ開始、指定したパスにファイルがぞろぞろ保存されます。

Delay は{% include link.html title="ImageMagick" url="http://www.imagemagick.org/" blank=1 %}に設定する値と同じもの（1/100秒）を入れられるようにしました。  

### パスの指定
![Edit Path](https://uranuno.github.io/PlayRecorder/save_capture.png)

ファイル名はDateTime をフォーマットするように。  
というわけで連番というのはウソなのですが、ミリ秒まで含めれば重複しないしImage Magick 動くしいいか、と思いました・・・

`EditorUtility.SaveFilePanel` を使っているので、「File Path」の「Edit」ボタンを押すと画像のようにパネルがでます。  
キャプチャ用フォルダをつくりつつパスとして指定する、というのができるのが便利です。  


いまいちなところ
----------------
いちいちScene に置かないと使えないのがちょっと面倒・・・  
{% assign ref=page.refs[2] %}{% include link.html param=ref title="公式リファレンスのEditorWindow.Update() に載っているサンプルコード" blank=1 %}を参考にEditorWindow 版をつくってみたりしたのですが、EditorWindow のフレームレートとGameView 内のフレームレートが違っていて、キャプチャのタイミングが調整しづらかったので、仕方なくそうしています、、
