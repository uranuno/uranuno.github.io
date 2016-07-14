---
title: PlayerPrefs をちょっとだけ拡張
refs:
  - title: ['uranuno/MyUnityUtils/PlayerPrefsData.cs', 'GitHub']
    url  : 'https://github.com/uranuno/MyUnityUtils/blob/master/Assets/Utils/PlayerPrefsData.cs'
  - title: ['Scripting API: PlayerPrefs', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/PlayerPrefs.html'
  - title: ['Scripting API: JsonUtility', 'Unity']
    url  : 'https://docs.unity3d.com/ScriptReference/JsonUtility.html'
---

[PlayerPrefs]({{ page.refs[1].url }}) をちょっとだけ拡張して、:point_down:みたいな書き方ができるようになる[PlayerPrefsData.cs]({{ page.refs[0].url }}) という汎用クラスをつくりました。  

```csharp
// 端末に保存したいデータのクラス（例: 音量の設定）
public class AudioSettings
  : PlayerPrefsData<AudioSettings> //←これをつくった
{
  public float bgmVolume = 1f; //デフォルト値も入れられる
  public float seVolume  = 1f;
}

// 使い方
public class PlayerPrefsDataExample : MonoBehaviour
{
  [SerializeField] Slider m_BgmVolumeSlider;
  [SerializeField] Slider m_SeVolumeSlider;

  void OnEnable  ()                    { LoadData (); }
  void OnDisable ()                    { SaveData (); }
  void OnApplicationPause (bool pause) { if (pause) SaveData (); }

  // データ読み込み
  void LoadData ()
  {
    // 保存データの読込
    // ※なければデフォ値の入った新規データを取得する（保存もされる）
    var data = AudioSettings.Load ();
    // UIに反映
    m_BgmVolumeSlider.value = data.bgmVolume;
    m_SeVolumeSlider.value = data.seVolume;
  }

  // データ書き込み
  void SaveData ()
  {
    // 新規データを作成
    var data = new AudioSettings ();
    // UIから値を取得
    data.bgmVolume = m_BgmVolumeSlider.value;
    data.seVolume = m_SeVolumeSlider.value;
    // 保存
    data.Save ();
  }
}
```

`PlayerPrefsData` を継承したデータクラスをつくって、端末に保存したい値をもたせておけば、あとは `Load()` `Save()` を呼ぶだけ、素で書くよりはラク！というもの。

<!-- more -->

PlayerPrefs は端末にデータをさくっと保存できて便利ですが、

* `int` `float` `string` タイプしか無い。それ以外は自分で変換しないといけない（大体 `bool` を `0,1` にする）
* データを読み込むとき、データが存在しなかったら、データを新しくつくって・・・みたいな分岐を書かないといけない
* 保存キーが文字列なのでどこかで管理しないといけない

この辺の処理を入れたラッパーを毎回つくるのが面倒・・・  
処理をまとめるにしても、保存したい値全部入りのデータベースみたいなクラスをつくってしまうと、プロジェクトごとに作り直しになるので、それも面倒・・・

[Unity5.3〜 のJsonUtility]({{ page.refs[2].url }}) を使えば、Json文字列化が簡単にできるから、全部string 扱いで一緒に処理できるかも、と思ってつくってみたのがこれです。

ミソは、保存キーにクラス名を使うので、自分で定義しなくてよいところです。  
1クラス1データになるけど、複数保存したいデータは、それを配列にもたせたデータクラスをつくって保存すればいいかなと思います。

ジェネリック便利、個人的には満足:smile:
