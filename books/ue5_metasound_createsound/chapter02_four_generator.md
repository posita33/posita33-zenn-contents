---
title: "4つのジェネレータと合成"
---

## 4つのジェネレータと合成

### 4つのジェネレータ

前回作成した MetaSoundを複製して、[MS_Procedual06]を作成します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-29-07-58-06.png)
*MS_Procedual05を右クリック > Dupulicate*

同じMIDI Note Noが再生されるように、Randomの接続を解除します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-29-07-59-59.png)
*同じMIDI Note Noが再生されるようにRandomの接続を解除する*

4つのジェネレータを追加します。

- Saw
- Sine
- Square
- Triangle

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-29-08-07-51.png)
*[Saw] [Sine] [Square] [Triangle]を追加する*

各ジェネレータのFrequencyに[MIDI To Frequency(Int32)：Out Frequency]を接続します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-29-08-12-58.png)
*各ジェネレータのFrequencyに[MIDI To Frequency(Int32)：Out Frequency]を接続*

Ladder Filterの下あたりを右クリックし、[Crossfade(Audio, 4)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-06-55-51.png)
*各ジェネレータのFrequencyに接続 > 右クリック > Crossfade(Audio, 4)*

[Crossfade(Audio, 4):Out]と[Ladder Fillter:In]を接続します。
[Crossfade(Audio, 4)]のInputピンに各ジェネレータのAudioを接続します。
・In 0：Sine
・In 1：Saw
・In 2：Square
・In 3：Triangle

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-06-59-17.png)
*各ジェネレータのAudioをSwitchのInputに接続*

[Crossfade(Audio, 4):Crossfade Value]をInput化します。
[Crossfade(Audio, 4):Crossfade Value]をドラッグ&ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-04-34.png)
*[Crossfade(Audio, 4):Crossfade Value]からドラッグ＆ドロップ > Promote To Graph Input*

Input Nameを[Generateor Type 01]に設定します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-07-16.png)
*Input Name：Generator Type 01*

[Play]ボタンを押してから、[Generator Type 01]のDefault Valueを変更することで、各ジェネレータの音の違いを確認できます。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-10-30.png)
*[Play]をクリック > Gererator Type 01のDefault Valueを変更*

### ジェネレータを合成する（Add）

ジェネレータを合成するように編集します。
Generatorの切り替え処理をすべて選択して、コピー&ペーストします。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-14-57.png)
*Generatorの切り替え処理をすべて選択して、コピー＆ペースト*

[Crossfade(Audio, 4):Crossfade Value]のInputを新しく作成します。
Input Nameは[Generator Type 02]に設定します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-16-19.png)
*[Crossfade(Audio, 4):Crossfade Value]をInput化 > Input Nameは[Generator Type 02]に設定*

左側のGeneratorのFrequencyを少し高くしてFrequencyをずらします。
左側の[MIDI To Frequncy(Int32)：MIDI In]からドラッグ&ドロップし、[Add(Int32)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-22-33.png)
*MIDI To Frequncy(Int32)：MIDI Inからドラッグ＆ドロップ > Add(int32)*

デフォルト値:60にし、AddのB側をInput化します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-25-08.png)
*Add(Audio) A：60 > Bからドラッグ＆ドロップ > Promote To Grapth Input*

Input Nameを[Detune]に設定し、Default Valueを[6]に設定します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-27-10.png)
*Input Name：Detune、Default Value：6*

右側の[Crossfade(Audio, 4):Out]からドラッグ&ドロップし、[Add(Audio)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-19-28.png)
*右側の[Crossfade(Audio, 4):Out]からドラッグ＆ドロップ > [Add(Audio)]を追加*

2つの音がAddで合成されるように接続します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-28-58.png)

PlayしてGenerator Typeを1,2で変えてみると音に厚みが出ます。

https://twitter.com/posita33/status/1469801120046657536

### 2つのジェネレータ合成をCrossfadeでずらす

Crossfadeで2つの合成音をずらしてみます。
音の合成処理をコピー&ペーストします。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-31-54.png)
*音の合成処理をコピー＆ペースト*

コピー&ペーストした側の[Crossfade(Audio, 4):Crossfade Value]を設定するInputを作り直します。
右側を[Generator Type 03]、左側を[Generator Type 04]になるように作り直します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-35-41.png)
*右側を[Generator Type 03]、左側を[Generator Type 04]になるように作り直す*

上側の合成処理（Add）から[Crossfade(Audio,2)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-38-32.png)
*Add(Audio)のOutからドラッグ＆ドロップ > Crossfade(Audio,2)*

[Crossfade(Audio,2)：Crossfade Value]をInput化します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-40-00.png)
*Crossfade(Audio,2)：Crossfade Value > ドラッグ＆ドロップ*

Input Nameを[Crossfade]、Defaultを[0.1]に設定します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-41-33.png)
*Input Name：Crossfade、Default：0.1*

2つの合成処理をCrossfadeで出力するように接続し直します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-43-12.png)
*二つの合成処理をCrossfadeで出力するように接続し直す*

[Play]ボタンで再生し、Generator TypeやCrossfadeの値を変更して音を確認します。

https://twitter.com/posita33/status/1469807434554548225

### ランダムなMIDI Note Noを送受信する

今までが単音だったので、MIDI Note Noをランダムになるように編集します。
今回はVariable（変数）を作成して値を受け渡します。

MembersのVariablesに変数を追加します。
Variableに[MIDI Note]、Typeに[Int32]を設定します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-47-50.png)
*Variablesの＋ボタンをクリック > 名前を[MINI Note]  Typeを[Int32]に設定*

[Random(int)]の右側くらいを右クリックし、[Set MIDI Note]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-52-50.png)
*[Random(int)]の右側くらいを右クリック > [Set MIDI Note]を追加*

[Random(Int)：Value]と[MIDI Note]を接続します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-54-20.png)
*Random(Int)：ValueとMIDI Noteを接続*

上側の合成処理の左側で右クリックし、[Get MIDI Note]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-07-56-57.png)
*右クリック > Get MIDI Note*

[MIDI Note]の値で左側と右側の[MIDI To Frequency：MIDI In]が変更されるように接続します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-08-00-40.png)
*[MIDI Note]の値で左側と右側の[MIDI To Frequency：MIDI In]が変更されるように接続*

下側の合成処理側にも[MIDI Note]の値で左側と右側の[MIDI To Frequency：MIDI In]が変更されるように接続します。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-08-03-58.png)
*下側も[Get MIDI Note]を追加 > 左側と右側の[MIDI To Frequency：MIDI In]が変更されるように接続します。*

[Play]ボタンをクリックし、再び1小節ごとに音がランダムに再生されることを確認します。
ここまでがプロシージャルの音作りになります。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-08-06-04.png)
*全体図*

## Generatorノードについて

4つのGeneratorノードについて解説します。（パラメータについては随時加筆します。）

- Saw
- Sine
- Square
- Triangle

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-09-30-08-06-49.png)
*Generatorの4つの波形タイプ*

4つのノードの違いは「波形の形」が違います。

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-02-20-10-45-34.png)
*波形の違い*

【Bi Polarについて】

> オーディオ周波数を -1.0 から 1.0 の間で出力します。False の場合、 0.0 から 1.0 の間の単極の値を出力します。
> 引用：MetaSound の参照ガイド Generator ノードの入力

![](/images/books/ue5_metasound_createsound/chapter02_four_generator/2022-02-20-10-46-19.png)
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
