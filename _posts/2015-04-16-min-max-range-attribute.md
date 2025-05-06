---
category: Unity
title: 値の最小値と最大値をいい感じに入力するPropertyDrawer
description: Random.Range とかの範囲をスライダーで入力できるようにしたいです。
modified_date: 2015-10-27
---

[MinMaxSlider といういい感じのEditorGUI][MinMaxSliderRef] があります。  
[一定の値の範囲からランダムな値を取得したいとき][RandomRangeRef]なんかに、このスライダーをつかって範囲を調整できたらいいな〜と思ったので、構造体 + PropertyDrawer をつくりました。  

[MinMaxSliderRef]: https://docs.unity3d.com/ScriptReference/EditorGUI.MinMaxSlider.html
[RandomRangeRef]: http://docs.unity3d.com/ScriptReference/Random.Range.html

<figure>
  <img src="https://uranuno.github.io/UnityUtils/minmaxrange.gif" alt="Unity Inspector上で範囲スライダーを動かして数値を変えるアニメGIF" width="400" />
  <figcaption>がんばってつくったGIF</figcaption>
</figure>

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

**uranuno/UnityUtils #MinMax**  
<https://github.com/uranuno/UnityUtils#min-max>

↑自作のUtility系をまとめたリポジトリをつくりました。

<!-- more -->


## 地味にこだわったところ

元から用意されている`Range` 属性をつけた値と並べたときにきれいになるよう大きさを揃えました・・・

```csharp
[SerializeField, MinMaxRange(0,10f)]
MinMax randomDelayRange;

[Range(0,10f)]
public float otherValue;
```

<img src="https://uranuno.github.io/UnityUtils/minmaxrange-othervalue.png" alt="並べてもスライダーの長さが揃ってきれい" width="400" />


## 他参考

- [Unity - Manual: Property Drawers](https://docs.unity3d.com/Manual/editor-PropertyDrawers.html)
