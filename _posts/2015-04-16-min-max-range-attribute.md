---
title: 値の最小値と最大値をいい感じに入力するPropertyDrawer
tags: [unity]
refs:
  - title: 'Scripting API: EditorGUI.MinMaxSlider - Unity'
    url  : 'https://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html'
  - title: 'Manual: Property Drawers - Unity'
    url  : 'https://docs.unity3d.com/Manual/editor-PropertyDrawers.html'
  - title: 'Tutorial: Property Drawers & Custom Inspectors - Unity'
    url  : 'https://unity3d.com/learn/tutorials/modules/intermediate/live-training-archive/property-drawers-custom-inspectors'
commits:
  - date : 2015-10-27
    title: 'Vector2 -> MinMax構造体'
    id   : 0fc6780159e1d1caf6f65a20051acd12bb2a8d1a
---

![Min Max Range Attribute](https://uranuno.github.io/MyUnityUtils/minmaxrange.gif "がんばってつくったGIF")

```csharp
[SerializeField, MinMaxRange(0,10f)]
MinMax randomDelayRange;

float delay;
float accum;

void Update () {
	accum += Time.deltaTime;

	if (accum >= delay) {
		Debug.Log ("Fire!");
		accum = 0;
		delay = randomDelayRange.randomValue;
	}
}
```

Unity には、[MinMaxSlider というすてきなEditorGUI](http://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html) があります。  
[一定の値の範囲からランダムな値を取得したいとき](http://docs.unity3d.com/ScriptReference/Random.Range.html)なんかに、このスライダーをつかって範囲を調整できたらいいな〜と思っていたので、構造体 + PropertyDrawer をつくりました。  

[uranuno/MyUnityUtils #MinMax](https://github.com/uranuno/MyUnityUtils#min-max)  
↑自作のUtility系をまとめたリポジトリをつくってみました。

<!-- more -->

地味にこだわったところ
--------------------
元から用意されている`Range` 属性をつけた値と並べたときにきれいになるよう大きさを揃えました・・・

```csharp
[SerializeField, MinMaxRange(0,10f)]
MinMax randomDelayRange;

[Range(0,10f)]
public float otherValue;
```

![With Other Value](https://uranuno.github.io/MyUnityUtils/minmaxrange-othervalue.png)
