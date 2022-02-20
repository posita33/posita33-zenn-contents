---
title: "サウンドの減衰（Sound Attenuation）について"
---

## 4章開始の準備

### フォルダを作成する

フォルダを作成します。

```
Content/
  └ MetaSoundSettings/
     ├ Audio/
     └ Maps/
```

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-21-36.png)

### Levelを別名で保存する

この章ではLevelを変更します。
ThirdPersonのレベルはそのまま残しておきたいので、別名でLevelを保存します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-34-17.png)
*File > Save Current Level As...*

Mapsフォルダに「MetaSoundSettings」で保存します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-37-49.png)

Project Settingsで[Editor Startup Map]を変更し、プロジェクトを開始時のLevelに設定します。
プロジェクトを閉じても開始時に設定したLevelが開くので編集しやすくなります。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-39-29.png)
*Edit > Project Settings...*

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-40-53.png)
*Maps & Modes > Editor Startup Mapを[MetaSoundSettings]に変更する*

## 配置したMetaSoundからの距離で聴こえ方を変える

同じ音源が何度も再生されていた方が、キャラクターを動かして距離による聴こえ方の違いが分かりやすいので、1つの音源をループ再生するMetaSoundを作成します。
1章で作成した「MS_Explosion」を複製して、「MS_Explosion1」を作成します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-56-37.png)

[MetaSoundSettins/Audio]に複製してできた「MS_Explosion1」を移動します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-20-58-02.png)

Explosion01をLoop再生するMetaSoundに修正します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-03-05.png)
*同じ音源をLoop再生するMetaSoundに修正する*

MetaSound[MS_Explosion1]をビューポートに配置して、[Play]ボタンをクリックします。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-06-14.png)
*ビューポートに[MS_Explosion1]を配置して、[Play]ボタンをクリック*

キャラクターをMetaSoundから近づけても、遠ざけても聞こえる音源の音量は同じに聞こえます。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-06-58.png)
*音源からの距離は関係なく同じ音量で聞こえる*

距離に応じて聴こえ方を変えるために、Sound Attenuation[ATT_Explosion]を作成します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-10-41.png)
*Sounds > Sound Attenuation[ATT_Explosion]を作成する*

[MS_Explosion1]を開き、[General]ボタンをクリックします。
[Attenuation Settings]に[ATT_Explosion]を設定します。 

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-14-03.png)
*MS_Explosion1の [Attenuation Settings]に[ATT_Explosion]を設定*

[Attenuation Settings]に[ATT_Explosion]を設定したMS_Explosion1を選択すると二つのSphere（球）が表示されます。
MS_ExplosionをFloorの角に移動して、外側の球がギリギリ対角線に入るくらいになるようにして、再び[Play]ボタンをクリックします。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-44-48.png)
*MS_Explosion1をFloorの角に移動する*

プレイした時にMS_Explosion1の距離に応じて音の聴こえ方が変わるのが分かります。
音源から離れるほど音が遠ざかって聴こえるようになります。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-45-05.png)
*音源の距離に応じて音の聴こえ方が変わる*

## サウンドの減衰(Sound Attenuation)のVolume設定について

Sound Attenuationアセットにはたくさん設定がありますが、今回はVolumeの減衰についてのみ変更します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-45-42.png)
*ATTENUATION(VOLUME)のプロパティを変更する*

まずはSphereの形状を設定する設定である、[Inner Radius]と[Falloff Distance]についてです。
[Inner Radius]を[400.0]から[500.0]に変更すると、内側の球の大きさが大きくなります。Unreal Engineの単位は1uu(Unreal Unit)=1cmなので、半径(radius)が4m(400cm)から5m(500cm)に変化したので球が大きくなりました。
[Falloff Distance]を[3600.0]から[2000.0]に変更すると、外側の球が小さくなりました。[Falloff Distance]の数値はInner Radiusの球の外側から、外側の球までの長さになります。

**[Inner Radius]+[Falloff Distance]=外側の球の半径**

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-46-44.png)
*Innner RadiusとFalloff Distanceの数値について*

Innner Radius内とFalloff Distance内のFalloff Distance外(外側の球の外)の音の聴こえ方についてです。
・Inner Radius内：音源そのままのVolume
・Falloff Distance内：音の減衰が始まる（遠くなるほどVolumeが小さくなる）
・Falloff Distance外：音が聞こえなくなる
外側の円は音が聞こえる範囲とも言えます。
Inner RadiusとFalloff DistanceはAttenuationの範囲を指定するプロパティです。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-47-04.png)
*Inner Radius内とFalloff Distance内外のVolumeについて*

次に[Attenuation Shape]を[Box]に変更します。
2つのSphere(球)は形状がBoxに変わります。形状がBoxに変わったことで、Inner RadiusがExtentに変わり、内側の形状を設定する項目が変わりました。
形状が変わることで内側の形状を変えるプロパティが変化します。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-47-18.png)
*Attenuation ShapeをBoxに変更すると、Sphere（球）からBoxに形状が変化する*

[Attenuation Shape]には[Sphere(球)]、[Capsule]、[Box]、[Cone]の4つの形状を選択することが出来ます。それぞれ、内側の形状の設定とそこから減衰する距離を設定できるようになっています。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-51-20.png)
*形状は[Sphere(球)]、[Capsule]、[Box]、[Cone]の4種類*

最後に[Attenuation Function]です。
[Attenuation Function]は音がどのように減衰するかを設定するプロパティになります。
デフォルトで設定されている[Linear]は直線的に減衰します。Falloff Distanceの中間では半分のVolumeになります。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-51-35.png)
*Attenuation Function：Linear*

[Attenuation Function]を[Logarithmic]に変更すると、減衰がカーブを描いて変化します。近づくほど変化が大きくなり、遠くになるとゆっくり減衰していきます。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-51-52.png)
*Attenuation Function：Logarithmic*

他にも減衰を設定するカーブのプリセットが用意されています。Customは自分で独自のカーブを作成することが出来ます。その他のカーブのプリセットは公式ドキュメントにどのようなカーブを描くか書かれていますので設定を変更してプレイしたりしながら確認してみましょう。

![](/images/books/ue5_metasound_createsound/chapter04_sound_attenuation/2022-02-20-21-52-10.png)
*Attenuation Functionは5種類+Custom*

https://docs.unrealengine.com/4.27/ja/WorkingWithAudio/DistanceModelAttenuation/