---
category: Unity
title: Tag とLayer を楽に入力するPropertyDrawer
---

Unity で、Tag とLayer をInspector から楽に入力できるように、PropertyDrawer をつくりました。

```csharp
// 属性を付けると
[Tag] public string targetTag;
[Layer] public int targetLayer;
```

<figure class="ar-3-2 top">
  <img src="https://uranuno.github.io/UnityUtils/tagandlayer.png" alt="Unity Inspector にTag とLayer のプルダウンが表示されているスクリーンショット" width="400" />
  <figcaption>Inspector がこんなかんじに</figcaption>
</figure>


{:.no_toc}
## 目次

{:toc}
- TOC


## Tag を手打ちしたくない

```csharp
void OnTriggerEnter (Collider other)
{
  if (other.tag == "Player")
    Debug.Log ("Hit!");
}
```

↑Tag の判定を単純に書くとこんな感じ  
`"Player"` は文字列なので、タイプミスしてても動かないだけでエラーは出ないし、打つときに補完も出ない・・・


## NameCreator を使ってみる

```csharp
void OnTriggerEnter (Collider other)
{
  // Tagだったら、「TagName」というクラスを自動生成してくれるので、
  // コードからタイプセーフに扱えるようになる。便利。
  if (other.tag == TagName.Player)
    Debug.Log ("Hit!");
}
```

Unityがもっている文字列情報から、静的クラスを自動生成してくれるというNameCreator というのを試してみました。  
これでタイプミスもしないし、補完も出るしいい感じ。

- [anchan828/namecreator](https://github.com/anchan828/namecreator)


## Inspector でも入力したい

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
Editorから静的クラスのプロパティが取得できたので、[NameCreator用のPropertyDrawerを自作][NameCreatorPropertyDrawer]してみたりしました。

[NameCreatorPropertyDrawer]: https://gist.github.com/uranuno/8be43847015f5e25cf17


## Editor からTag とLayer が取得できた

ところが、こんなもの[EditorGUI.TagField] を発見・・・  
あれ？Editor のクラスに、Tag を表示する関数あったの？  
静的クラスつくらなくても、表示できるの？

* * *

というわけでPropertyDrawerをつくりなおしました。

ついでに、[EditorGUI.LayerField] というのもあったので入れました。  
下記のように値に属性をつけるだけで、Inspector で楽に入力できるようになります。

[EditorGUI.TagField]: https://docs.unity3d.com/ScriptReference/EditorGUI.TagField.html
[EditorGUI.LayerField]: https://docs.unity3d.com/ScriptReference/EditorGUI.LayerField.html

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

<figure class="ar-3-2 top">
  <img src="https://uranuno.github.io/UnityUtils/tagandlayer-tag.png" alt="プルダウンでTag が選べる" width="400" />
  <figcaption>Tag が選べる :)</figcaption>
</figure>

<figure class="ar-4-3 top">
  <img src="https://uranuno.github.io/UnityUtils/tagandlayer-layer.png" alt="プルダウンでLayer が選べる" width="400" />
  <figcaption>Layer が選べる :)</figcaption>
</figure>

静的クラス生成方式は結構大掛かりなので、TagとLayerのみでいい、Inspectorで入力するからコード補完もいらない、という場合はこれだけでいいのかも。

**uranuno/UnityUtils #TagAndLayerAttribute**  
<https://github.com/uranuno/UnityUtils#tag-and-layer-attribute>
