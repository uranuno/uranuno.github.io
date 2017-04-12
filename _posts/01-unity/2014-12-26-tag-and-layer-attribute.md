---
category: unity
title: Tag とLayer を楽に入力するPropertyDrawer
refs:
  - title: ['uranuno/UnityUtils #TagAndLayerAttribute', 'GitHub']
    url  : 'https://github.com/uranuno/UnityUtils#tag-and-layer-attribute'
  - title: ['anchan828/namecreator', 'GitHub']
    url  : 'https://github.com/anchan828/namecreator'
  - title: ['Scripting API: EditorGUI.TagField', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/EditorGUI.TagField.html'
  - title: ['Scripting API: EditorGUI.LayerField', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/EditorGUI.LayerField.html'
---

![Tag and Layer Attribute](https://uranuno.github.io/UnityUtils/tagandlayer.png)

```csharp
[Tag]
public string targetTag;

[Layer]
public int targetLayer;
```

Unity で、Tag とLayer をInspector から楽に入力できるように、PropertyDrawer をつくりました。

[{{ page.refs[0].title[0] }}]({{ page.refs[0].url }}){:target="_blank"}

<!-- more -->

Tag を手打ちしたくない
----------------------
```csharp
void OnTriggerEnter (Collider other)
{
  if (other.tag == "Player")
    Debug.Log ("Hit!");
}
```

↑Tag の判定を単純に書くとこんな感じ  
`"Player"` は文字列なので、タイプミスしてても動かないだけでエラーは出ないし、打つときに補完も出ない・・・


NameCreator をつかってみる
--------------------------
```csharp
void OnTriggerEnter (Collider other)
{
  // Tagだったら、「TagName」というクラスを自動生成してくれるので、
  // コードからタイプセーフに扱えるようになる。便利。
  if (other.tag == TagName.Player)
    Debug.Log ("Hit!");
}
```

Unityがもっている文字列情報から、静的クラスを自動生成してくれるという[NameCreator]({{ page.refs[1].url }}){:target="_blank"} というのを試してみました。  
これでタイプミスもしないし、補完も出るしいい感じ。


Inspector でも入力したい
------------------------
```csharp
// [Name(typeof(クラス名))]という属性を付けると、Inspector上でPopupで選べるように！
[Name(typeof(TagName))] public string playerTag;

void OnTriggerEnter (Collider other)
{
  if (other.tag == playerTag)
    Debug.Log("Hit!");
}
```

いまさらですが、Inspector で値を入力するのがすきです。（タイプミスが、補完が、とか言ってたのに・・・）  
Editorから静的クラスのプロパティが取得できたので、[NameCreator用のPropertyDrawerを自作](https://gist.github.com/uranuno/8be43847015f5e25cf17){:target="_blank"}してみたりしました。


Editor からTag とLayer が取得できた
-----------------------------------
ところがこんなもの（[EditorGUI.TagField]({{ page.refs[2].url }}){:target="_blank"}）を発見・・・  
あれ？Editor のクラスに、Tag を表示する関数あったの？  
静的クラスつくらなくても、表示できるの？

・・・

というわけでPropertyDrawerをつくりなおしました。

ついでに、[EditorGUI.LayerField]({{ page.refs[3].url }}){:target="_blank"} というのもあったので入れました。  
下記のように値に属性をつけるだけで、Inspector で楽に入力できるようになります。

```csharp
[Tag] public string targetTag;
[Layer] public int targetLayer;

void OnTriggerEnter (Collider other)
{
  if (other.tag == targetTag)
  {
    Debug.Log("Hit!");
    // 別レイヤーに移動するとか
    other.gameObject.layer = targetLayer;
  }
}
```

![Tag Attribute](https://uranuno.github.io/UnityUtils/tagandlayer-tag.png)
![Layer Attribute](https://uranuno.github.io/UnityUtils/tagandlayer-layer.png)

静的クラス生成方式は結構大掛かりなので、TagとLayerのみでいい、Inspectorで入力するからコード補完もいらない、という場合はこれだけでいいのかも。
