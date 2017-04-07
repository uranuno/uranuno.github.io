---
title: 値の最小値と最大値をいい感じに入力するPropertyDrawer
refs:
  - title: ['uranuno/MyUnityUtils #MinMax', 'GitHub']
    url  : 'https://github.com/uranuno/MyUnityUtils#min-max'
  - title: ['Scripting API: EditorGUI.MinMaxSlider', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html'
  - title: ['Manual: Property Drawers', 'Unity']
    url  : 'https://docs.unity3d.com/Manual/editor-PropertyDrawers.html'
  - title: ['Tutorial: Property Drawers & Custom Inspectors', 'Unity']
    url  : 'https://unity3d.com/learn/tutorials/modules/intermediate/live-training-archive/property-drawers-custom-inspectors'
commit:
  date : 2015-10-27
  title: 'Vector2 -> MinMax構造体'
  id   : 0fc6780
---

[MinMaxSlider といういい感じのEditorGUI]({{ page.refs[1].url }}){:target="_blank"} があります。  
[一定の値の範囲からランダムな値を取得したいとき](http://docs.unity3d.com/ScriptReference/Random.Range.html){:target="_blank"} なんかに、このスライダーをつかって範囲を調整できたらいいな〜と思ったので、構造体 + PropertyDrawer をつくりました。  

![Min Max Range Attribute](https://uranuno.github.io/MyUnityUtils/minmaxrange.gif "がんばってつくったGIF")

```csharp
[SerializeField, MinMaxRange(0,10f)]
MinMax randomDelayRange;

float delay;
float accum;

void Update ()
{
  accum += Time.deltaTime;
  if (accum >= delay)
  {
    Debug.Log ("Fire!");
    accum = 0;
    delay = randomDelayRange.randomValue;
  }
}
```

[{{ page.refs[0].title[0] }}]({{ page.refs[0].url }}){:target="_blank"}  
↑自作のUtility系をまとめたリポジトリをつくりました。

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

![With Other Value](https://uranuno.github.io/MyUnityUtils/minmaxrange-othervalue.png "並べてもきれい")
