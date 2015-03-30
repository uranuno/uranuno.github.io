---
layout: post
title: Unity で最小値と最大値をスライダーで入力できるようにするPropertyDrawer
tag: [unity3d]
---

![Image](https://dl.dropboxusercontent.com/u/18856747/Screenshot/20150327_1.png)

[gist - MinMaxRangeAttribute](https://gist.github.com/uranuno/36d27d9f5d9a5ee389cc)

Unity には、[MinMaxSlider というすてきなEditorGUI](http://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html) があります。  
ゲームをつくるとき、一定の値の範囲からランダムな値を取得したいときがよくあるのですが、
そのときこのスライダーをつかって範囲を調整したいな〜と思っていたので、PropertyDrawer をつくりました。  

<!-- more -->

使い方は下記のようになります。

{% gist 36d27d9f5d9a5ee389cc MinMaxRangeAttributeTest.cs %}
 
MinMax 的なクラスをつくるか迷ったのですが、気軽に使いたいので（この属性がなくても動く）とりあえずVector2 をつかってます。

あとはしぬほど地味ですが、元から用意されている`[Range(0, 10f)]` のような属性をつけた値と並べたときにきれいになるよう大きさを揃えました・・・

![Image](https://dl.dropboxusercontent.com/u/18856747/Screenshot/20150330_1.png)


参考
-----
- [Unity - Manual: Property Drawers](http://docs.unity3d.com/Manual/editor-PropertyDrawers.html)
- [Unity - Property Drawers & Custom Inspectors](https://unity3d.com/learn/tutorials/modules/intermediate/live-training-archive/property-drawers-custom-inspectors)
