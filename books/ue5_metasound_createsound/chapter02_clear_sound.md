---
title: "音をクリアにする"
---

## 音をクリアにする

### 音をクリアにするノードを組み上げる

まずはノードを組んでから、使用したノードについて調べていきます。
今日使用するのは[**Ladder Filter**],[**LFO**],[**WaveShaper**]ノードです。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-53-05.png)
*[Ladder Fillter] [LFO] [WaveShaper]*

前回作成した MetaSoundを複製して、[MS_Procedual03]を作成します。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-57-20.png)
*MS_Procedual02を右クリック > Duplicate*

[ADSR Envelope(Audio)]から[AD Envelope(Audio)]を使用するように修正します。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-58-01.png)
*ADSR Envelope(Audio)からAD Envelope(Audio)を使用するように修正*

[Sine：Audio]からドラッグ&ドロップし、[Ladder Filter]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-58-27.png)
*[Sine：Audio]からドラッグ＆ドロップ > Ladder Filter*

[Ladder Filter：Cutoff Frequency]からドラッグ&ドロップして[LFO]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-58-44.png)
*[Ladder Filter：Cutoff Frequency]からドラッグ＆ドロップ > LFO*

[Ladder Filter：Ount]からドラッグ&ドロップして[WaveShaper]を追加する。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-58-58.png)
*Ladder Filter：Outからドラッグ＆ドロップ > WaveShaper*

[WaveShpaer：Out]と[AD Envelope(Audio)：Ont Envelope]を掛け合わせる音を再生するように接続する。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-17-59-16.png)
*[WaveShpaer：Out]と[AD Envelope(Audio)：Ont Envelope]を掛け合わせる音を再生する*

各ノードの値を変更します。

【LFO】

| Property    | Value  |
| ----------- | ------ |
| Frequency   | 0.5    |
| Min Value   | 500.0  |
| Max Value   | 5000.0 |
| Pulse Width | 0.8    |

【Ladder Filter】

| Property  | Value |
| --------- | ----- |
| Resonance | 2.0   |

【WaveShaper】

| Property | Value           |
| -------- | --------------- |
| Amount   | 2.0             |
| Bias     | 0.6             |
| Type     | Inverse Tangent |


![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-02-26.png)
*各ノードの値を変更する*

SineのAudioを直接再生するよりクリアな音を再生できます。

https://twitter.com/posita33/status/1468451854032207876

それでは、各ノードについて何が行われているのか学習してみます。

### Ladder Filterについて

まずは【Ladder Filter】について調べてみましょう。
パラメーターとして用意されているのは[Cutoff Frequency]と[Resonance]です。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-05-40.png)
*Ladder Filter*

公式ドキュメントの【**Ladder Filter**】の説明文です。

> Ladder Filter ノードは、仮想アナログ ローパス フィルタ(Low-pass filter)で、心地よくクラッシックなロールオフ(Roll Off)とレゾナンス(Resonance)があります。


【**Cutoff Frequencyについて**】

まずはローパスフィルター(Low-pass filter)が何かを調べてみました。
ローパスフィルターはCutoff Frequencyで指定した値（周波数）を基準に扱いが変わります。

| Cutoffの値                   | 説明                          |
| ---------------------------- | ----------------------------- |
| Cutoff Frequencyより小さい値 | そのままの値を通します。      |
| Cutoff Frequencyより大きい値 | Gainが0.0になるまで減衰します |

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-07-47.png)
*Low-pass filter：低い周波数は通すのでLowをPassするフィルター*

https://www.g200kg.com/jp/docs/dic/lowpassfilter.html

次に【Resonance】のプロパティについてです。
Resonanceはカットオフ周波数付近の音を強調させるパラメーターです。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-08-48.png)
*Resonanceはカットオフ周波数付近の音を強調させる*

https://www.youtube.com/watch?v=XA_WnyA7D6k

https://www.newdtm-rain.com/article/446212175.html

Cutoff Frequencyしか設定できない、[One-Pole Low Pass Filter]と[One-Pole High Pass Filter]も用意されています。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-09-59.png)
*Cutoff Frequencyしか設定できない、[One-Pole Low Pass Filter]と[One-Pole High Pass Filter]*

High Pass FilterはCutoff Frequencyをより大きい周波数はそのままの音にするFilterです。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-10-27.png)
*High Pass FilterはCutoff Frequencyより大きい周波数を通すフィルター*

他にも2種類フィルターは用意されていますが、今回はLow Pass FilerとHigh Pass Filterについて理解できたのでいずれ使用してみます。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-10-51.png)
*Bitquad FilterとState Variable Filter*

### LFO（Low Frequency Oscillator：低周波オシレーター）について

次に【**LFO**】について調べていきます。
YouTubeでMetaSoundのメイキングを真似していると必ず出てくるノードです。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-11-17.png)
*LFO*

色々調べたのですが、まだ良く分からないので、今回は解るところまででもう少し詳しくなったら再挑戦します。
[Phase Offse]と[Pulse Width]は値を変えても違いが分からなかったので、もう少し公式ドキュメントが充実したらあらためてLFOについて書きます。

公式ドキュメントの【LFO】の説明文です。

> Low Frequency Oscillator (LFO) ノードは複数のジェネレータ形状に加え出力範囲マッピング、位相オフセット、パルス幅 (矩形波 LFO) に対応しています。同期トリガーは LFO 位相を開始時の位相オフセットにリセットします。

一番分かりやすいのが【Shape】です。
ShapeはLFOの波形の形状を決定します。
Sine（正弦波）、Square（矩形波）、Triangle（三角波）、Saw（ノコギリ波）の4種類があります。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-12-15.png)
*Shape(4種類の波形)*

https://www.youtube.com/watch?v=YEHnd9b79Uc

https://note.com/masatsumu/n/n42aab8563422

【**Frequency**】
周波数の1周期を[1.0]として、[5.0]になると1周期で5回になるといったパラメーターです。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-13-15.png)
*Frequencyの動き*

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-13-43.png)
*LFOのOut(Float)をAudioに変えて再生してみて調べてみました。*

[Max Value]と[Min Value]ですが、良く分かりませんでした。

【Max ValueとMin Valueの絶対値が同じ場合】
音（タと書いてある文字）の出るタイミングが同じで、数値が大きくなるにつれてVolumeが大きくなりました。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-14-12.png)
*Max ValueとMin Valueの絶対値が同じ場合は数値が大きくなるにつれてVolumeが大きくなる*

【MinValueを0.0に設定し、MaxValueの値を変えた場合】

MaxValueの値を2倍にしていくと、音（タと書いてある文字）のタイミングが早くなっていきました。周期は同じなので、音がなってからの空白が少しずつ増えていきました。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-14-31.png)
*Min Valueが0.0の時にMax Valueを変えた時の音の変化*

https://zynaddsubfx.sourceforge.io/doc/html/lfo/lfo.html

https://www.elektronauts.com/t/lfo-depth-question/39721/2

よくつかうノードだけに詳しく書きたかったのですが、DTMで使われているLFOに書かれている名称とパラメーター名が違うので合っているのか分かりませんでした。

### WaveShaperについて

最後に【WaveShaper】について調べていきます。

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-15-33.png)
*WaveShaper*

公式ドキュメントに【WaveShaper】の説明がありませんでした。
LFO同様にもう少し公式ドキュメントが充実したらまとめます。
WaveShaperは波形の変形や成型する機能だそうです。
Typeの形状と青い線で出力するLevelをクリップできるようです。
[Amount]、[Bias]、[OutputGain]で青い線を作成するのではないでしょうか？

![](/images/books/ue5_metasound_createsound/chapter02_clear_sound/2022-02-19-18-15-48.png)
*WaveShaperのイメージ*

https://www.g200kg.com/jp/docs/dic/waveshaper.html

https://www.g200kg.com/jp/docs/webaudio/waveshaper.html