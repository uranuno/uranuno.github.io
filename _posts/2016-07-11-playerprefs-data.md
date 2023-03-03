---
category: Unity
title: PlayerPrefs をちょっとだけ拡張
modified_date: 2017-04-10
---

[PlayerPrefs][PlayerPrefsRef] をちょっとだけ拡張して、👇みたいな書き方ができるようになる汎用クラスをつくりました。

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
    var data = PlayerPrefsData<AudioSettings>.Load (
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
    PlayerPrefsData<AudioSettings>.Save (data);
  }

  // データのリセット
  void ResetData ()
  {
    // データの削除
    PlayerPrefsData<AudioSettings>.Delete ();
    // データの再読み込み（未保存状態のため、デフォルト値になる）
    LoadData ();
  }
}
```

![とりあえずのUI][PlayerPrefsDataView]{:standalone width="400" height="400"}

端末に保存したいデータのクラスをつくって、あとは `PlayerPrefsData<T>.Load()` `PlayerPrefsData<T>.Save()` などを呼ぶだけ、素で書くよりはラク！というもの。

<!-- more -->

PlayerPrefs は端末にデータをさくっと保存できて便利ですが、

- `int` `float` `string` タイプしか無い。それ以外は自分で変換しないといけない（大体 `bool` を `0,1` にする）
- 保存キーが文字列なのでどこかで管理しないといけない

この辺の処理を入れたラッパーを毎回つくるのが面倒・・・  
処理をまとめるにしても、保存したい値全部入りのデータベースみたいなクラスをつくってしまうと、プロジェクトごとに作り直しになるので、それも面倒・・・

[Unity5.3〜 のJsonUtility][JsonUtilityRef] を使えば、Json文字列化が簡単にできるから、全部string 扱いで一緒に処理できるかも、と思ってつくってみたのがこれです。

保存キーにクラス名を使うので、自分で定義しなくていいのが良いところです。  
1クラス1データになるけど、複数保存したいデータは、それを配列にもたせたデータクラスをつくって保存すればいいかなと思います。

ジェネリックすごく便利、個人的には満足😄

[**uranuno/UnityUtils #PlayerPrefsData**][UnityUtilsPlayerPrefsData]


[PlayerPrefsRef]: https://docs.unity3d.com/ScriptReference/PlayerPrefs.html
[PlayerPrefsDataView]: https://uranuno.github.io/UnityUtils/playerprefsdata.png

[JsonUtilityRef]: https://docs.unity3d.com/ScriptReference/JsonUtility.html

[UnityUtilsPlayerPrefsData]: https://github.com/uranuno/UnityUtils#playerprefs-data
