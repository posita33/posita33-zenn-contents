---
title: "風の音を作成する"
---

## 風の音を作成する

### ベースとなる風の音を作成する

前回作成した MetaSoundを複製して、[MS_Noise02]を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-11-45-40.png)
*MS_Noise01を右クリック > Dupulicate > [MS_noise02]に名前を変更*

ノード追加の説明を省いて、Node名、変化のあるパラメータ名と値を書きます。

【Noise】

|Parameter|Value|
|---|---|
|Type|White Nose|

【Biquad Filter】

|Parameter|Value|
|---|---|
|Bandwidth|0.1|
|Type|Butterworth Low Pass|

【LFO】

|Parameter|Value|
|---|---|
|Frequency|1.0|
|Min Value|150.0|
|Max Value|200.0|

これだけでも風の音が聞こえます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-11-46-35.png)
*風の音*

風の強さを変更できるように[Multiply(Float)：B]をインプット化します。
Input Nameは[Wind Strength]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-30-10.png)
*風の強さを変更できるInput：[Wind Strength]を作成する*

https://twitter.com/posita33/status/1470744110810419202

環境音としては少し音が単調なので、音をランダムに振幅させます。
0.5秒間隔でLFOのFrequencyを[0.0～1.0]の値で変化させます。
LFOのFrequencyを変更させると速度が変わるので、風に少し速度が付いたように聞こえます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-31-15.png)
*0.5秒間隔でLFOのFrequencyを[0.0～1.0]の値で変化させて、風にランダムな速度を付ける*

### 別の風の音を作成する

風をもう2つ作成します。

【Noise】

|Parameter|Value|
|---|---|
|Type|White Nose|

【Envelope Follower】

|Parameter|Value|
|---|---|
|Attack Time|3.0|
|Release Time|1.0|

【LFO 2】

|Parameter|Value|
|---|---|
|Min Value|400.0|
|Max Value|600.0|

【LFO 3】

|Parameter|Value|
|---|---|
|Min Value|0.8|
|Max Value|1.1|

【Biquad Filter】

|Parameter|Value|
|---|---|
|Type|Butterworth Low Pass|

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-35-26.png)
*別の風の作り方*

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-45-52.png)
*数値が分かる画像*

https://twitter.com/posita33/status/1470752009074937858

今度はLFOの波形を[Triangle]に変更した風の音を作成します。

【LFO 4】

|Parameter|Value|
|---|---|
|Min Value|300.0|
|Max Value|600.0|


[Biquad Filter]

|Parameter|Value|
|---|---|
|Band Width|0.4|
|Type|Low Pass|

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-43-07.png)
*LFOの波形を[Triangle]にした風を作成する*

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-49-34.png)
*数値が分かる図*

https://twitter.com/posita33/status/1470754188657590274

### 風の音を重ねる

3つの風の音を重ねることで自然な音にします。
MonoMixer(3)で3つの音を重ねます。
風の音はそれぞれ大きさを別々にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-50-23.png)
*風1,2,3をMono Mixerで重ねる*

1つの音だけでも風の音に聞こえましたが、複数の音が重なることでより自然な音になりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter03_wind/2022-02-20-18-53-26.png)
*完成図*
