---
layout: post
title: 値の範囲をスライダーで入力できるようにするPropertyDrawer
tag: [unity3d]
---

![Min Max Range Attribute](http://uranuno.github.io/MyPropertyDrawers/minmaxrange.gif "がんばってつくったGIF")

```csharp
[SerializeField, MinMaxRange(0,10f)]
Vector2 randomDelayRange;

float randomDelay { get { return Random.Range(randomDelayRange.x, randomDelayRange.y); } }
	
float delay;
float accum;

void Update () {
	accum += Time.deltaTime;

	if (accum >= delay) {
		Debug.Log ("Fire!");
		accum = 0;
		delay = randomDelay;
	}
}
```

Unity には、[MinMaxSlider というすてきなEditorGUI](http://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html) があります。  
[一定の値の範囲からランダムな値を取得したいとき](http://docs.unity3d.com/ScriptReference/Random.Range.html)なんかに、このスライダーをつかって範囲を調整できたらいいな〜と思っていたので、PropertyDrawer をつくりました。  

[uranuno/MyPropertyDrawers #MinMaxRangeAttribute - :octocat:](https://github.com/uranuno/MyPropertyDrawers#min-max-range-attribute)  
↑自作のPropertyDrawer をまとめる用のリポジトリをつくってみました。

<!-- more -->

地味にこだわったところ
--------------------
元から用意されている`Range` 属性をつけた値と並べたときにきれいになるよう大きさを揃えました・・・

```csharp
[SerializeField, MinMaxRange(0,10f)]
Vector2 randomDelayRange;

[Range(0,10f)]
public float otherValue;
```

![With Other Value](http://uranuno.github.io/MyPropertyDrawers/minmaxrange-othervalue.png)


参考
-----
- [Scripting API: EditorGUI.MinMaxSlider - Unity](http://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html)
- [Manual: Property Drawers - Unity](http://docs.unity3d.com/Manual/editor-PropertyDrawers.html)
- [Tutorial: Property Drawers & Custom Inspectors - Unity](https://unity3d.com/learn/tutorials/modules/intermediate/live-training-archive/property-drawers-custom-inspectors)
