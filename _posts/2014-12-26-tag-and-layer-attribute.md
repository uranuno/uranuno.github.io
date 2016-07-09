---
title: Tag とLayer を楽に入力するPropertyDrawer
tags: [unity]
---

![Tag and Layer Attribute](https://uranuno.github.io/MyUnityUtils/tagandlayer.png)

```csharp
[Tag]
public string targetTag;

[Layer]
public int targetLayer;
```

Unity で、Tag やLayer をInspector から楽に入力できるように、PropertyDrawer をつくりました。

[uranuno/MyUnityUtils #TagAndLayerAttribute :octocat:](https://github.com/uranuno/MyUnityUtils#tag-and-layer-attribute)

<!-- more -->

Tag を文字列で手打ちしたくない
------------------------------
UnityでTagを利用するとき、単純に書くとこんな感じになります。

```csharp
void OnTriggerEnter(Collider other) {

    if(other.tag == "Player") {
        Debug.Log("Hit!");
    }
}
```

このとき「Player」を自分で打ちこむのはタイプミスの危険があるので、嫌です。

以前それを回避するために、[NameCreator](https://github.com/anchan828/namecreator)というのを使わせてもらって、静的クラスを生成する方法を試してみました。

```csharp
void OnTriggerEnter(Collider other) {

    // 例えばTagであれば、「TagName」というクラスが自動生成され、
    // コードからタイプセーフに扱えるようになる。便利。
    if(other.tag == TagName.Player) {
        Debug.Log("Hit!");
    }
}
```

さらに、[PropertyDrawerを自作して](https://gist.github.com/uranuno/8be43847015f5e25cf17)、Inspector上でも値が入力できるようにしてみたりもしました。

```csharp
// [Name(typeof(クラス名))]という属性を付けると、Inspector上でPopupで選べるように！
[Name(typeof(TagName))] public string playerTag;

void OnTriggerEnter(Collider other) {

    if(other.tag == playerTag) {
        Debug.Log("Hit!");
    }
}
```

ところがこんなもの（[EditorGUI.TagField](http://docs.unity3d.com/ScriptReference/EditorGUI.TagField.html)）を発見・・・  
あれ？Editorのクラスに、Tag を表示する関数あったの？  
静的クラスつくらなくても、表示できるの？

・・・

というわけでPropertyDrawerをつくりなおしました。

ついでに、[EditorGUI.LayerField](http://docs.unity3d.com/ScriptReference/EditorGUI.LayerField.html) というのもあったので入れました。  
下記のように値に属性をつけるだけで、Inspector で楽に入力できるようになります。

```csharp
[Tag] public string targetTag;
[Layer] public int targetLayer;

void OnTriggerEnter(Collider other) {

    if(other.tag == targetTag) {
        Debug.Log("Hit!");
        // 別レイヤーに移動するとか
        other.gameObject.layer = targetLayer;
    }
}
```

![Tag Attribute](https://uranuno.github.io/MyUnityUtils/tagandlayer-tag.png)
![Layer Attribute](https://uranuno.github.io/MyUnityUtils/tagandlayer-layer.png)

静的クラス生成方式は結構大掛かりなので、TagとLayerのみでいい、Inspectorで入力するからコード補完もいらない、という場合はこれだけでいいかもしれません。


参考
-----
- [anchan828/property-drawer-collection - GitHub](https://github.com/anchan828/property-drawer-collection)
- [Scripting API: PropertyDrawer - Unity](http://docs.unity3d.com/ScriptReference/PropertyDrawer.html)
