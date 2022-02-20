---
title: "4つのジェネレータと合成"
---

## 4つのジェネレータと合成

### 4つのジェネレータ

前回作成した MetaSoundを複製して、[MS_Procedual06]を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-24-30.png)
MS_Procedual05を右クリック > Dupulicate
同じMIDI Note Noが再生されるように、Randomの接続を解除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-26-34.png)
*同じMIDI Note Noが再生されるようにRandomの接続を解除する*

4つのジェネレータを追加します。

- Saw
- Sine
- Square
- Triangle

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-26-50.png)
*[Saw] [Sine] [Square] [Triangle]を追加する*

各ジェネレータのFrequencyに[MIDI To Frequency(Int32)：Out Frequency]を接続します。
Ladder Filterの下あたりを右クリックし、[Switch]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-27-07.png)
*各ジェネレータのFrequencyに接続 > 右クリック > Switch*

SwitchのInputピンに各ジェネレータのAudioを接続します。
・Input0：Sine
・Input1：Saw
・Input2：Square
・Input3：Triangle
[Switch：Selector]をInput化します。
[Switch：Selector]をドラッグ&ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-27-33.png)
*各ジェネレータのAudioをSwitchのInputに接続 > [Switch：Selector]からドラッグ＆ドロップ > Promote To Graph Input*

Input Nameを[Generateor Type 01]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-27-59.png)
*Input Name：Generator Type 01*

[Play]ボタンを押してから、[Generator Type 01]の値を変更することで、各ジェネレータの音の違いを確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-28-15.png)
*[Play]をクリック > Gererator Type 01のDefault Valueを変更*

### ジェネレータを合成する（Add）

ジェネレータを合成するように編集します。
Generatorの切り替え処理をすべて選択して、コピー&ペーストします。
SwitchのSelectorを変更していたInputは作り直します。Input Nameは[Generator Type 02]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-28-44.png)
*Generatorの切り替え処理をすべて選択して、コピー＆ペースト*

SwitchのSelectorを変更していたInputは作り直します。Input Nameは[Generator Type 02]
右側の[Switch：Output]からドラッグ&ドロップし、[Add(Audio)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-38-08.png)
*右側の[Switch：Output]からドラッグ＆ドロップ > [Add(Audio)]を追加*

左側のGeneratorのFrequencyを少し高くしてFrequencyをずらします。
左側の[MIDI To Frequncy(Int32)：MIDI In]からドラッグ&ドロップし、[Add(Int32)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-07-28-59.png)
*MIDI To Frequncy(Int32)：MIDI Inからドラッグ＆ドロップ > Add(int32)*

デフォルト値:60にし、AddのB側をInput化します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-38-40.png)
*Add(Audio) A：60 > Bからドラッグ＆ドロップ > Promote To Grapth Input*

Input Nameを[Detune]に設定し、Default Valueを[6]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-38-58.png)
*Input Name：Detune、Default Value：6*

2つの音がAddで合成されるように接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-59-08.png)

PlayしてGenerator Typeを1,2で変えてみると音に厚みが出ます。

https://twitter.com/posita33/status/1469801120046657536

### 2つのジェネレータ合成をCrossfadeでずらす

Crossfadeで2つの合成音をずらしてみます。
音の合成処理をコピー&ペーストします。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-40-59.png)
*音の合成処理をコピー＆ペースト*

コピー&ペーストした側の[Switch：Selector]を設定するInputを作り直します。
右側を[Generator Type 03]、左側を[Generator Type 04]になるように作り直します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-41-17.png)
*右側を[Generator Type 03]、左側を[Generator Type 04]になるように作り直す*

上側の合成処理（Add）から[Crossfade(Audio,2)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-41-40.png)
*Add(Audio)のOutからドラッグ＆ドロップ > Crossfade(Audio,2)*

[Crossfade(Audio,2)：Crossfade Value]をInput化します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-41-55.png)
*Crossfade(Audio,2)：Crossfade Value > ドラッグ＆ドロップ*

Input Nameを[Crossfade]、Defaultを[0.1]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-42-08.png)
*Input Name：Crossfade、Default：0.1*

2つの合成処理をCrossfadeで出力するように接続し直します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-42-25.png)
*二つの合成処理をCrossfadeで出力するように接続し直す*

[Play]ボタンで再生し、Generator TypeやCrossfadeの値を変更して音を確認します。

https://twitter.com/posita33/status/1469807434554548225

### ランダムなMIDI Note Noを送受信する

今までが単音だったので、MIDI Note Noをランダムになるように編集します。
今回は SendノードとReceiveノードで値を受け渡しします。

[Random(int)]の右側くらいを右クリックし、[Send Int32]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-43-05.png)
*Random(int)の右側くらいを右クリック > Send Int32*

[Random(Int)：Value]と[Send Int32：Int32]を接続します。
[Send Int32：Address]を[MIDI Note]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-43-22.png)
*Random(Int)：ValueとSend Int32：Int32を接続 > Send Int32：MIDI Note*

上側の合成処理の左側で右クリックし、[Receive Int32]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-43-36.png)
*右クリック > Receive Int32*

[Receive Int32：Default]を[60]に設定し、[Receive Int32：Address]を[MIDI Note]に設定します。
[Receive Int32：Out]を[MIDI to Frequency(Int32)：MIDI In]が変更されるように接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-43-56.png)
*[Receive Int32：Default]を[60]、[Receive Int32：Address]を[MIDI Note]に設定
[Receive Int32：Out]を[MIDI to Frequency(Int32)：MIDI In]が変更されるように接続*

[Receive Int32：Default]を下側の合成処理側にコピー&ペーストし、同様に接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-44-15.png)
*[Receive Int32：Default]を下側の合成処理側にコピー＆ペーストし、同様に接続*

[Play]ボタンをクリックし、再び1小節ごとに音がランダムに再生されることを確認します。
ここまでがプロシージャルの音作りになります。

## Generatorノードについて

4つのGeneratorノードについて解説します。（パラメータについては随時加筆します。）

- Saw
- Sine
- Square
- Triangle

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-45-20.png)
*Generatorの4つの波形タイプ*

4つのノードの違いは「波形の形」が違います。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-45-34.png)
*波形の違い*

【Bi Polarについて】

> オーディオ周波数を -1.0 から 1.0 の間で出力します。False の場合、 0.0 から 1.0 の間の単極の値を出力します。
> 引用：MetaSound の参照ガイド Generator ノードの入力

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_four_generator/2022-02-20-10-46-19.png)
*Bi PolarのON/OFF*

その他のパラメータは随時分かり次第加筆します。
以下のURLの音の説明が分かりやすかったです。

https://musicplanz.org/introduction-synthesizers/identity-and-nature-of-sound

## Crossfadeノード
Crossfadeノードは0.0～1.0でIn（入力値）の出力を変更するノードです。

> MetaSound は指定の入力間をブレンドするさまざまな Crossfade ノードを備えています。このノードは Crossfade Value (クロスフェード値) を使用して入力をブレンドします。例えば、入力値が 2 と 4 の Crossfade Value を 0.5 にすると、出力は 3 になります。
> 現時点では、このノードはブロック レートの浮動小数点パラメータによる線形クロスフェードのみに対応しています。将来的に、開発チームは一定パワーやカーブなどの非線形クロスフェードやオーディオ レート クロスフェードを追加する予定です。
> 引用：MetaSound の参照ガイド Crossfade ノード

https://twitter.com/posita33/status/1469978292153647108
