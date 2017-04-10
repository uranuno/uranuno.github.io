---
title: PlayerPrefs をちょっとだけ拡張
refs:
  - title: ['uranuno/MyUnityUtils #PlayerPrefsData', 'GitHub']
    url  : 'https://github.com/uranuno/MyUnityUtils#playerprefs-data'
  - title: ['Scripting API: PlayerPrefs', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/PlayerPrefs.html'
  - title: ['Scripting API: JsonUtility', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/JsonUtility.html'
commit:
  date : 2017-04-10
  title: 'PlayerPrefsData.cs をstatic に'
  id   : 65024b8
---

[PlayerPrefs]({{ page.refs[1].url }}){:target="_blank"}をちょっとだけ拡張して、:point_down:みたいな書き方ができるようになる汎用クラスをつくりました。

![PlayerPrefs Data](https://uranuno.github.io/MyUnityUtils/playerprefsdata.png "とりあえずのView")

```csharp
// 端末に保存したいデータのクラス（例: 音量の設定）
public class AudioSettings
{
  public float bgmVolume = 1f;
  public float seVolume  = 1f;
}
```

```csharp
// 使い方
public class PlayerPrefsDataExample : MonoBehaviour
{
  /* 中略 */

  void LoadData ()
  {
    // データの読込
    var data = PlayerPrefsData.Load<AudioSettings> (
      //データが未保存の場合のデフォルト値を指定できる
      new AudioSettings ()
    );
    // UIに反映
    m_BgmVolumeSlider.value = data.bgmVolume;
    m_SeVolumeSlider.value = data.seVolume;
  }

  void SaveData ()
  {
    // 新規データを作成
    var data = new AudioSettings ();
    // UIから値を取得
    data.bgmVolume = m_BgmVolumeSlider.value;
    data.seVolume = m_SeVolumeSlider.value;
    // データの保存
    PlayerPrefsData.Save<AudioSettings> (data);
  }

  // データのリセット
  void ResetData ()
  {
    // データの削除
    PlayerPrefsData.Delete<AudioSettings> ();
    // データの再読み込み（未保存状態のため、デフォルト値になる）
    LoadData ();
  }
}
```
[{{ page.refs[0].title[0] }}]({{ page.refs[0].url }}){:target="_blank"}

端末に保存したいデータのクラスをつくって、あとは `Load<T>()` `Save<T>()` などを呼ぶだけ、素で書くよりはラク！というもの。

<!-- more -->

PlayerPrefs は端末にデータをさくっと保存できて便利ですが、

* `int` `float` `string` タイプしか無い。それ以外は自分で変換しないといけない（大体 `bool` を `0,1` にする）
* 保存キーが文字列なのでどこかで管理しないといけない

この辺の処理を入れたラッパーを毎回つくるのが面倒・・・  
処理をまとめるにしても、保存したい値全部入りのデータベースみたいなクラスをつくってしまうと、プロジェクトごとに作り直しになるので、それも面倒・・・

[Unity5.3〜 のJsonUtility]({{ page.refs[2].url }}){:target="_blank"} を使えば、Json文字列化が簡単にできるから、全部string 扱いで一緒に処理できるかも、と思ってつくってみたのがこれです。

ミソは、保存キーにクラス名を使うので、自分で定義しなくてよいところです。  
1クラス1データになるけど、複数保存したいデータは、それを配列にもたせたデータクラスをつくって保存すればいいかなと思います。

ジェネリック便利、個人的には満足:smile:
