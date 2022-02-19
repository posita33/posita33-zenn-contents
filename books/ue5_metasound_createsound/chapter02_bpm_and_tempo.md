---
title: "BPMでテンポとリズムを作る"
---

## BPMでテンポとリズムを作る

### Trigger Repeatで一定間隔のテンポで再生する

使用するノードは[BPM To Seconds],[Trigger Repeat],[Trigger Counter]ノードです。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-34-28.png)
*[BPM To Seconds] [Trigger Repeat] [Trigger Counter]*

前回作成した MetaSoundを複製して、[MS_Procedual04]を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-41-17.png)
*MS_Procedual03を右クリック > Duplicate*

リズムを刻むので、単音がクリアに聞こえるように各ノードの数値を調整します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-43-37.png)
*各ノードの設定を調整した開始時の状態*

[Trigger Repeat]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-44-02.png)
*右クリック > Trigger Repeat*

[Trigger Repeat]を[Input：On Play]と[AD Envelope(Audio)]の間に実行されるように接続します。
[Ountput：On Finished]が呼び出されると停止してしまうので、[AD Envelope(Audio):On Done]と[Ountput：On Finished]の接続を解除して、ループするようにします。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-45-18.png)
*Trigger Repeatが実行されるように接続、On Finishedを呼び出さないようにしてループさせる*

Stopを制御するInput Triggerを作成します。
[Trigger Repeat：Stop]からドラッグ＆ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-45-39.png)
*Trigger Repeat：Stopからドラッグ＆ドロップ > Promote To Graph Input*

Input Nameを[On Stop]に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-45-52.png)
*Input Name：On Stop*

再生時に変化を確認しやすように、[Trigger Repeat：Period]をInput化します。
[Trigger Repeat：Repeat]からドラッグ＆ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-46-09.png)
*Trigger Repeat：Periodからドラッグ＆ドロップ > Promote To Graph Input*

Input Nameを[Period]に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-46-27.png)
*Input Name：Period*

[Input：On Stop]で[Trigger Repeat：Stop]で[Trigger Repeat]を停止させてから再び[Trigger Repeat：Start]を呼び出せるように[Input：On Replay]というTriggerInputを追加します。
[Input：On Play]からドラッグ＆ドロップし、 [Trigger Any(2)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-46-41.png)
*Input：On Playからドラッグ＆ドロップ > Trigger Any(2)*

[Trigger Any(2)：In 1]からドラッグ＆ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-46-54.png)
*[Trigger Any(2)：In 1]からドラッグ＆ドロップ > Promote To Graph Input*

Input Nameを[On Replay]にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-47-09.png)
*Input Name：On Replay*

[Play]をクリックして再生します。
[Input：Period]の[Default]を[1.0]に変更すると、1秒間隔で音が再生されます。
[Trigger Repeat：RepeatOut]はPeriodの値が[1.0]を1秒として、Periodで指定した時間(秒)で繰り返し実行されます。
ノードのパラメータをInput化しておくと、Play後に値を変えて音を確認出来るのでInput化は非常に便利です。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-47-24.png)
*Period 1.0の時、1秒ごとにTrigger Repeat：RepeatOutが実行される*

[Play]後に、[Input：On Stop]のSimulateボタンをクリックすると[Trigger Repeat：Stop]が実行され、Trigger Repeatが停止します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-47-41.png)
*[Play]後に、[Input：On Stop]のSimulateボタンをクリックすると
[Trigger Repeat：Stop]が実行され、Trigger Repeatが停止*

[Input：On Replay]のSimulateボタンを実行すると、[Trigger Repeat：Start]が実行され、再び[Trigger Repeat]が再生します。
[Input：On Play]はPlayボタンが押された時に1度だけ実行される特別なノードので、再生後にStart、StopをTriggerで実行したい時には、[Trigger Any]ノードを使用します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-48-04.png)
*[Input：On Replay]のSimulateボタンを実行すると、
[Trigger Repeat：Start]が実行され、再び[Trigger Repeat]が再生
[Input：On Play]はPlayボタンが押された時に1度だけ実行される特別なノード*

[Trigger Repeat]ノードを組み込んだ状態です。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-49-02.png)
*[Trigger Repeat]ノードを組み込んだ状態*

https://twitter.com/posita33/status/1468951170828083202

### BPM To SecondsでBPMを指定できるようにする

[**BPM To Seconds**]ノードは指定したBPM(Beat Per Minutes)の秒数を取得できるノードです。

> BPMは、曲の速さで4分音符を1分間に打つ回数のことをいいます。
> 引用：DTM音楽用語辞典078「BPM」とは？

https://masatsumu-dtm.com/word_78-bpm/

【**BMP To Secondsノードのインプットについて**】

| パラメータ              | 説明                                          |
| ----------------------- | --------------------------------------------- |
| BPM                     | BPMの指定(1分間に何回4分音符を打つか)         |
| Divisions of Whole Note | 4で4分音符、8で8分音符、16で16分音符          |
| Beat Multipier          | Beat Multipier：Secondsで出力する値に掛ける値 |

例)Secondsが1.0（秒）を出力する結果の時、Beat Multiplierが2.0の場合、Secondsは1.0 x 2.0 = 2.0(秒)になる

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-51-00.png)
*BPM To Seconds*

BPM To Secondsの動きを確認できるようにノードを組んでいきます。
[Trigger Repeat：Period]からドラッグ＆ドロップし、[BPM To Seconds]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-52-32.png)
*Trigger Repeat：Periodからドラッグ＆ドロップ > BPM To Seconds*

[Input：Period]はもう使用しないので削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-52-54.png)
*Input：Periodは削除*

[BPM To Seconds]のパラメータをすべてInput化します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-53-46.png)
*[BPM To Seconds]のパラメータをすべてInput化*

Input化したら、それぞれInput Nameを変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-54-07.png)
*Input Nameを変更する*

[BPM To Seconds]ノードを組み込んだ状態です。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-54-37.png)
*[BPM To Seconds]ノードを組み込んだ状態*

### Trigger CounterでMIDI Noteを1小節ごとにRandomに変更する

1小節ごとにMIDI Note Noをランダムに変更できるように組んでいきます。
[Input：On Play]から[Trigger Repeat]までの処理を左側に移動します。
[Trigger Repeat：RepeatOut]からドラッグ＆ドロップし、[Trigger Counter]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-55-09.png)
*[Trigger Repeat：RepeatOut]からドラッグ＆ドロップ > [Trigger Counter]を追加*

[Trigger Counter：On Reset]からドラッグ＆ドロップし、[Random(Int)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-55-23.png)
*[Trigger Counter：On Reset]からドラッグ＆ドロップ > [Random(Int)]を追加*

Random(int)のValueをMIDI Note Noとして使用するように設定します。

[**Trigger Conter**]
Reset Count：4

[**Randam(int)**]
Min：60
Max：70

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-55-54.png)
*Random(int)のValueをMIDI Note Noとして使用するように設定*

Reset Countを4にすると、5拍目が1拍目にリセットされます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-56-15.png)
*Reset Count 4の時のTrigger Counterの動き*

MIDI Note No. 60～71はド4～シ4なので、Random (int)に60～71になる値を設定しています。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-56-30.png)
*MIDI Note Noの音階一覧（ド４~ド５まで）*

[Trigger Counter]ノードを組み込んだ状態です。
これで、1小節ごとにTrigger CounterのResetが実行されRandomなMIDI Note Noが再生されるようになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter02_bpm_and_tempo/2022-02-19-18-56-46.png)
*[Trigger Counter]ノードを組み込んだ状態*

https://twitter.com/posita33/status/1468978903637454848
