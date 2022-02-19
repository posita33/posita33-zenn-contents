---
title: "ドの音を鳴らす"
---

## ドの音を再生する

### フォルダとMetaSoundを作成する

フォルダを作成します。

```
Content/
  └ MetaSoundProcedual/
     └ Audio/
```

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-46-22.png)

MataSound[MS_Procedual01]を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-47-43.png)
*右クリック > Sounds > MetaSound*

名前を[MS_Procedual01]に設定し、ダブルクリックしてMetaSoundを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-48-38.png)
*名前を[MS_Procedual01]に設定*

### Sine波を再生する

[Sine]ノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-51-01.png)
*右クリック > Sine*

[Sine：Audio]と[Output：Audio]を接続します。
[Play]を押すと音が再生されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-53-42.png)
*SineとOutputのAudioを接続すると音が再生される*

Frequencyは「周波数」です。
数値[440.0]は440Hz（ヘルツ）を意味します。
440Hzは1秒間に440回音が振幅します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-55-18.png)
*周波数 Hz（ヘルツ）について*

https://info.shimamura.co.jp/digital/knowledge/2014/03/19260/2

440Hzは「ラ」の音にあたり、「ラ」の音で音が流れ続けてます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-56-24.png)
*440Hzはラの音*

Hz（ヘルツ）の数値が大きくなるにつれて高い音になり、数値が低くなると低い音になります。ドレミといった音階には特定のHz（ヘルツ）があるんですね。

>音階は、「音を高低の順番に並べたもの」あり、音の高低は周波数で表します。
>音は、周波数が半分になると１オクターブ低くなり、周波数が倍になると１オクターブ高くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-57-02.png)
*Hzが大きくなると高い音、小さくなると低い音*

https://tomari.org/main/java/oto.html

### MIDI Note Noでド（C4）の音を再生する

MIDIのNote Noでド（C4）の周波数を取得して、ド（C4）の音を再生できるようにします。
[MIDI To Frequency(Int32)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-57-53.png)
*右クリック > MIDI To Frequency(Int32)*

[MIDI To Frequency(Int32)：Out Frequency]と[Sine：Frequency]を接続します。
[Play]ボタンを押すとドの音が再生されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-58-18.png)
*[MIDI To Frequency(Int32)のOut Frequency]と[SineのFrequency]を接続*

[MIDI To Frequency(Int32)：Out Frequency]の周波数を確認します。
[Print Log(Float)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-58-43.png)
*右クリック > Print Log(Float)*

[MIDI To Frequency(Int32)：Out Frequency]の数値をLogに出力します。
[Input：On Play]と[Print Log(Float)：Trigger]を接続します。
[MIDI To Frequency(Int32)：Out Frequency]を[Print Log(Float)：Value To Log]を接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-59-12.png)
*[MIDI To Frequency(Int32)：Out Frequency]の数値をLogに出力する*

[Print Log(Float)]のLog出力は[Output Log]ウィンドウに出力されます。
[Output Log]は[Windows]メニューから[Output Log]を選択することで表示できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-17-06-51.png)

261.625549が出力されていたので、[MIDI To Frequency(Int32)：Out Frequency]の周波数は261.625549Hz（ヘルツ）ということが分かりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-16-59-35.png)
*[Print Log(Float)]のLog出力は[Output Log]ウィンドウに出力される*

261.625549Hz（ヘルツ）はド4（C4）の音の周波数(261.626)とほぼ一致しています。
これでドの音を再生していると判断できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-17-00-02.png)
*ド4(C4)の周波数とほぼ一致する*

[MIDI To Frequency(Int32)：MIDI In]の数値はMIDIのNote Noを指定しています。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-17-00-22.png)
*MIDI Inの数値はMIDI Note No*

MIDI Note Noの[60]はド4（C4）なので、ド4（C4）の周波数である[261.626]を取得できます。
MIDI Note Noは数値で特定の音階を指定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_play_c_sound/2022-02-19-17-00-45.png)
*MIDI Note Noの[60]はド4(C4)なので、ド4(C4)の周波数である[261.626]を取得できる*

https://izmi.com/doc/d002_noteno-hz.html

https://ja.wikipedia.org/wiki/MIDI

