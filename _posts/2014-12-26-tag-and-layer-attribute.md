---
category: unity
title: Tag とLayer を楽に入力するPropertyDrawer
source:
  title: ['uranuno/UnityUtils #TagAndLayerAttribute', 'GitHub']
  url  : 'https://github.com/uranuno/UnityUtils#tag-and-layer-attribute'
refs:
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

{% assign source=page.source %}{% include link.html param=source blank=1 %}

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

{% assign ref = page.refs[0] %}
Unityがもっている文字列情報から、静的クラスを自動生成してくれるという{% include link.html param=ref title="NameCreator" blank=1 %}というのを試してみました。  
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
Editorから静的クラスのプロパティが取得できたので、{% include link.html title="NameCreator用のPropertyDrawerを自作" url="https://gist.github.com/uranuno/8be43847015f5e25cf17" blank=1 %}してみたりしました。


Editor からTag とLayer が取得できた
-----------------------------------
{% assign ref = page.refs[1] %}
ところがこんなもの（{% include link.html param=ref title="EditorGUI.TagField" blank=1 %}）を発見・・・  
あれ？Editor のクラスに、Tag を表示する関数あったの？  
静的クラスつくらなくても、表示できるの？

・・・

というわけでPropertyDrawerをつくりなおしました。

{% assign ref = page.refs[2] %}
ついでに、{% include link.html param=ref title="EditorGUI.LayerField" blank=1 %}というのもあったので入れました。  
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
