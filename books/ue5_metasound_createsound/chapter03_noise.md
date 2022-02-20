---
title: "Noiseノードについて"
---

## Noiseノードについて

### フォルダを作成する

フォルダを作成します。

```
Content/
  └ MetaSoundSample/
     └ Audio/
```

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-19-18-53.png)

### Noiseノードを再生する

[Noise]ノードは環境音やBeat音を作る時に欠かせないノードです。
[Noise]ノードはどのような音が再生されるか簡単に説明します。

Content Drawerから右クリックし、MetaSound[MS_Noise01]を作成します。

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-11-29-37.png)
*右クリック > Sounds > > MetaSound > 名前を[MS_Noise01]に設定*

[Noise]ノードを追加します。

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-11-30-34.png)
*右クリック > Noise*

[Noise：Audio]を[Output：Audio]に接続します。
[Play]ボタンをクリックし、[Noise]ノードを再生します。

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-11-31-02.png)

[Noise：Audio]を[Output：Audio]に接続 > [Play]ボタンをクリックし、[Noise]ノードを再生
NoseのTypeは2種類あるので、Typeの違いについて調べましょう。

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-11-31-22.png)
*NoiseのTypeは2種類[Pink Noise]、[White Noise]*

## Pink Noise

同じ周波数成分を持つ光がピンク色に見えることからピンクノイズと呼ばれるそうです。(波長が短い音は赤色)

> パワーが周波数に反比例するノイズ
> 「ザー」と聞こえる
> 引用：【FAQ】ホワイトノイズとピンクノイズ

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-11-32-16.png)
*Pink Noise*

https://twitter.com/posita33/status/1470383348648673282

## White Noise

ホワイトノイズはすべての周波数で同じ強度になるノイズです。
ホワイトノイズという名前があったので、その他のノイズにも色の名前が付けられたそうです。

> 全ての周波数で同じ強度となるノイズ
>「シャー」と聞こえる
>【FAQ】ホワイトノイズとピンクノイズ

![](/images/books/ue5_metasound_createsound/chapter03_noise/2022-02-20-11-33-11.png)

https://twitter.com/posita33/status/1470383546338791429
