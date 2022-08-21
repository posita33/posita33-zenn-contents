---
title: "Envelopeを使ってアタック音を再生する"
---

## Envelopeを使ってアタック音を再生する
### AD Envelope(Audio)でアタック音を再生する

前回作成した[MS_Procedual01]を複製して、[MS_Procedual02]を作成します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-18-50-14.png)
*[MS_Procedual01]をDuplicate(複製)して、[MS_Procedual02]を作成する*

[AD Envelope(Audio)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-18-51-55.png)
*右クリック > AD Envelope(Audio)*

[Input：On Play]と[AD Envelope(Audio)]を接続します。
Print Log(Float)は削除します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-18-53-03.png)
*[Input：On Play]と[AD Envelope(Audio)]を接続*

[AD Envelope(Audio)：Out Envelope]と[Sine：Audio]を掛け算(Multiply)する処理を実装します。
[AD Envelope(Audio)：Out Envelope]からドラッグ&ドロップし、[Multiply(Audio)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-18-54-41.png)
*AD Envelope(Audio)からドラッグ＆ドロップ > Multiply(Audio)*

[AD Envelope(Audio)：Out Envelope]と[Sine：Audio]を掛け算(Multiply)した結果を[Output：Audio]に接続します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-18-59-42.png)
*[AD Envelope(Audio)：Out Envelope]と[Sine：Audio]を掛け算(Multiply)した結果を[Output：Audio]に接続*

https://twitter.com/posita33/status/1468043276112764928

AD Envelopeの[Attack Time]と[Decay Time]を分かりやすくした図です。

| 名称        | 概要                                                 |
| ----------- | ---------------------------------------------------- |
| Attack Time | Envelope Valueが1.0になるまでの時間                  |
| Decay Time  | Envelope Valueが1.0になってから、0.0になるまでの時間 |

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-02-19-17-28-35.png)
*Attack TimeとDecay Timeについて*

Sineノード単体では「ド～」とずっと再生されていました。
SineノードにAD Envelopeを掛け算することで「ド」と短い音（アタック音）が聞こえるようになります。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-02-19-17-28-52.png)
*SineノードにAD Envelopeを掛け算することで「ド」をアタック音として再生させる*

AD Envelopeの[Attack Curve]と[Decay Curve]を分かりやすくした図です。
デフォルト値の[1.0]はLinear（1.0）で数値が変化します。
[1.0]より値が小さくなるとカーブが[Logarithmic（対数）]のカーブに変わります。
[1.0]より値が大きくなるとカーブが[Exponential（指数関数）]のカーブになります。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-02-19-17-29-14.png)
*Curveの形状*

https://twitter.com/posita33/status/1468110908501401604

https://www.sparknotes.com/math/calcab/logs/section4/

https://www.perfectcircuit.com/signal/learning-synthesis-envelopes-1


最後に[Looping]のチェックボックスをチェックし、[On Finished]を呼び出さないようにします。
[AD Envelope(Audio)：On Done]が呼ばれるタイミングで、再び[AD Envelope(Audio)：Trigger]が呼ばれてループします。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-19-01-45.png)
*[AD Envelope(Audio)：Looping]にチェック > On Finesedを呼び出さないようにする*

[AD Envelope(Audio)：On Done]で[Output：On Finished]を呼び出すとMetaSoundを停止するのでループは行われません。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-19-03-09.png)
*On Finishedを呼び出すとMetaSoundが停止（強制終了）扱いになるのでループしない*

https://twitter.com/posita33/status/1468118043494854661

AD Envelopeは太鼓のバチで叩いた時のようなアタック音を再現する時に使うようです。

### ADSR Envelope(Audio)でアタック音を再生する

Envelopeノードは[AD Envelope]と[ADSR Envelope]の2種類が用意されています。
[ADSR Envelope(Audio)]を試してみましょう。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-19-04-42.png)
*右クリック > ADSR Envelope(Audio)*

[ADSR Envelope(Audio)：Audio]と[Sine：Audio]を掛け合わせた音を再生するように編集します。
[AD Envelope]より[ADSR Envelope]の方が細かく値を設定できることが分かります。
この状態で再生しても[ADSR Envelope(Audio)：On Done]が実行されず、[Sine：Audio]が実行された状態になります。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-19-08-17.png)
*[ADSR Envelope(Audio)：Audio]と[Sine：Audio]を掛け合わせた音を再生するように編集*

[ADSR Envelope(Audio)：Trigger Release]を実行するように[Input：On Release]を追加しましょう。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-21-25-26.png)
*[ADSR Envelope(Audio)：Trigger Release]からドラッグ＆ドロップ > Promote To Graph Input*

[Input]を[On Release]に変更します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-21-28-50.png)
*Input：On Releaseに変更*

[Play]後に[On Release]をSimuleteすると、Trigger Release > On Done > On Finishが呼ばれて停止します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-21-32-53.png)
*[Play]後に[On Release]をSimuleteすると、
Trigger Release > On Done > On Finishが呼ばれて停止する*

ADSR Envelopeにも[Attack Time]と[Decay Time]があります。さらに[Sustain Level]と[ReleaseTime]が追加されています。[Attack][Decay][Sustain][Release]の頭文字をとると[ADSR]になります。
ADRのTimeとSustain Levelについて分かりやすい図を用意しました。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-02-19-17-37-32.png)
*[Attack Time][Decay Time][Release Time]と[Sustain Level]について*

Trigger Releaseが呼ばれるまでSustain Levelの数値でSineのAudioが再生されるので、再生され続けていたことが分かりました。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-02-19-17-37-56.png)
*Trriger Releaseが実行されないと Sustain Levelの値が継続する*

[Sustain]の状態にも時間を指定してみます。
[Trigger Delay]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-21-37-57.png)
*右クリック > Trigger Delay*

Sustain Timeが[0.2（秒）]になるように[Trigger Delay：Delay Time]に[0.41]を設定します。
[Play]を押すと、[0.41]秒後に[ADSR Envelope(Audio)：Trigger Release]が実行されるようになります。
Sustain Timeを求める数式です。

**Sustain Time = Delay Time - (Attack Time + Decay Time)**
0.2 = 0.41 - (0.01 + 0.2)

Inputに[Attack Time],[Decay Time],[Sustain Time]を作成して、Delay Timeを求めるように計算します。

**Delay Time = Attack Time + Decay Time + Sustain Time**
0.41 = 0.01 + 0.2 + 0.2

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-08-21-21-40-53.png)
*Sustain Time = Delay Time - (Attack Time + Decay Time)*

ADSR Envelopeでは[Attack Curve]と[Decay Curve]の他に[Release Curve]が追加されます。分かりやすくした図を作成しました。
デフォルト値の[1.0]はLinear(1.0)で数値が変化します。
[1.0]より値が小さくなるとカーブが[Logarithmic（対数）]のカーブに変わります。
[1.0]より値が大きくなるとカーブが[Exponential（指数関数）]のカーブになります。

![](/images/books/ue5_metasound_createsound/chapter02_Envelope/2022-02-19-17-39-03.png)
*Curveの形状*

ADSR Envelopeはピアノの鍵盤のように押した時に音が出て（Attack > Decay）、指を押させている間は音が出続け(Sustain)、指を鍵盤から離した時に徐々に音が消えていく（Release）という状態遷移を再現する時に使うようです。

http://iphonedtm.blog.fc2.com/blog-entry-17.html
