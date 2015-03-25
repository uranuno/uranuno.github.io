---
layout: post
title: Tag とLayer をInspector 上で楽に入力するPropertyDrawer
tag: [unity]
---

UnityでTagを利用するとき、単純に書くとこんな感じになります。

{% highlight csharp %}
void OnTriggerEnter(Collider other) {
    if(other.tag == "Player") {
        Debug.Log("Hit!");
    }
}
{% endhighlight %}

このとき「Player」を自分で打ちこむのはタイプミスの危険があるので、嫌だと思っている人は多いかと思います。

<!-- more -->

以前それを回避するために、[NameCreator](https://github.com/anchan828/namecreator)というのを利用させてもらって、静的クラスを生成する方法を取ってみました。

{% highlight csharp %}
void OnTriggerEnter(Collider other) {
    // 例えばTagであれば、「TagName」というクラスが自動生成され、
    // コードからタイプセーフに扱えるようになる。便利。
    if(other.tag == TagName.Player) {
        Debug.Log("Hit!");
    }
}
{% endhighlight %}

さらに、[PropertyDrawerを自作して](https://gist.github.com/uranuno/8be43847015f5e25cf17)（staticなプロパティの中身はEditorスクリプトから取得可能だった）、Inspector上でも楽に値が入力できるようにしてみたりもしました。

{% highlight csharp %}
// [Name(typeof(クラス名))]という属性を付けると、Inspector上でPopupで選べるように！
[Name(typeof(TagName))] public string playerTag;

void OnTriggerEnter(Collider other) {
    if(other.tag == playerTag) {
        Debug.Log("Hit!");
    }
}
{% endhighlight %}

ところが最近こんなもの（[EditorGUI.TagField](http://docs.unity3d.com/ScriptReference/EditorGUI.TagField.html)）を発見・・・  
あれ？Editorのクラスに、Tag を表示する関数あったの？

・・・

というわけでPropertyDrawerをつくりなおしました。

{% gist 3793dbfcaa023525bdac TagAndLayerAttribute.cs %}

ついでに、[EditorGUI.LayerField](http://docs.unity3d.com/ScriptReference/EditorGUI.LayerField.html) というのもあったので入れました。  
使い方は下記のようになります。

{% highlight csharp %}
[Tag] public string playerTag;
[Layer] public int escapeLayer;

void OnTriggerEnter(Collider other) {
    if(other.tag == playerTag) {
        Debug.Log("Hit!");
        // 別レイヤーに移動するとか
        other.gameObject.layer = escapeLayer;
    }
}
{% endhighlight %}

![ss1](https://dl.dropboxusercontent.com/u/18856747/Screenshot/20141226_1_ss.png)
![ss2](https://dl.dropboxusercontent.com/u/18856747/Screenshot/20141226_2_ss.png)

静的クラス生成方式は結構大掛かりなので、TagとLayerのみでいい、Inspectorで入力するからコード補完もいらない、という場合はこれだけでいいかもしれません。


* * *
## 便利なPropertyDrawer
- [property-drawer-collection](https://github.com/anchan828/property-drawer-collection)
- [【Unity】正規表現を使用してstring型の値を制限する「RegexAttribute」](http://baba-s.hatenablog.com/entry/2014/03/06/131112)
