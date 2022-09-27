---
title: "BPMでテンポとリズムを作る"
---

## BPMでテンポとリズムを作る

### Trigger Repeatで一定間隔のテンポで再生する

使用するノードは[BPM To Seconds],[Trigger Repeat],[Trigger Counter]ノードです。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-02-19-18-34-28.png)
*[BPM To Seconds] [Trigger Repeat] [Trigger Counter]*

前回作成した MetaSoundを複製して、[MS_Procedual04]を作成します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-21-22-34-21.png)
*MS_Procedual03を右クリック > Duplicate*

リズムを刻むので、単音がクリアに聞こえるように各ノードの数値を調整します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-00-26.png)
*各ノードの設定を調整した開始時の状態*

[Trigger Repeat]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-02-02.png)
*右クリック > Trigger Repeat*

[Trigger Repeat]を[Input：On Play]と[AD Envelope(Audio)]の間に実行されるように接続します。
[Ountput：On Finished]が呼び出されると停止してしまうので、[AD Envelope(Audio):On Done]と[Ountput：On Finished]の接続を解除して、ループするようにします。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-04-19.png)
*Trigger Repeatが実行されるように接続、On Finishedを呼び出さないようにしてループさせる*

Stopを制御するInput Triggerを作成します。
[Trigger Repeat：Stop]からドラッグ＆ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-06-10.png)
*Trigger Repeat：Stopからドラッグ＆ドロップ > Promote To Graph Input*

Inputを[On Stop]に変更します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-07-55.png)
*Input：On Stop*

再生時に変化を確認しやすように、[Trigger Repeat：Period]をInput化します。
[Trigger Repeat：Repeat]からドラッグ＆ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-09-54.png)
*Trigger Repeat：Periodからドラッグ＆ドロップ > Promote To Graph Input*

[Input：On Stop]で[Trigger Repeat：Stop]で[Trigger Repeat]を停止させてから再び[Trigger Repeat：Start]を呼び出せるように[Input：On Replay]というTriggerInputを追加します。
[Input：On Play]からドラッグ＆ドロップし、 [Trigger Any(2)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-13-11.png)
*Input：On Playからドラッグ＆ドロップ > Trigger Any(2)*

[Trigger Any(2)：In 1]からドラッグ＆ドロップし、[Promote To Graph Input]を選択します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-15-00.png)
*[Trigger Any(2)：In 1]からドラッグ＆ドロップ > Promote To Graph Input*

Inputを[On Replay]にします。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-16-42.png)
*Input：On Replay*

[Input:On Play]と[Trigger Any(2):in 0]を接続します
![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-08-22-08-17-51.png)
*[Input:On Play]と[Trigger Any(2):in 0]を接続*

[Play]をクリックして再生します。
[Input：Period]の[Default]を[1.0]に変更すると、1秒間隔で音が再生されます。

![](/images/books/book-ue5_mathematical_programming/chapter02_bpm_and_tempo/2022-09-25-21-28-36.png)

[Trigger Repeat：RepeatOut]はPeriodの値が[1.0]を1秒として、Periodで指定した時間(秒)で繰り返し実行されます。
ノードのパラメータをInput化しておくと、Play後に値を変えて音を確認出来るのでInput化は非常に便利です。

![](/images/books/book-ue5_mathematical_programming/chapter02_bpm_and_tempo/2022-09-25-21-31-08.png)
*Period 1.0の時、1秒ごとにTrigger Repeat：RepeatOutが実行される*

![](/images/books/book-ue5_mathematical_programming/chapter02_bpm_and_tempo/2022-09-25-21-34-44.png)
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

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-07-59-22.png)
*BPM To Seconds*

BPM To Secondsの動きを確認できるようにノードを組んでいきます。
[Trigger Repeat：Period]からドラッグ＆ドロップし、[BPM To Seconds]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-00-49.png)
*Trigger Repeat：Periodからドラッグ＆ドロップ > BPM To Seconds*

[Input：Period]はもう使用しないので削除します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-03-30.png)
*Input：Periodは削除*

[BPM To Seconds]のパラメータをすべてInput化します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-05-07.png)
*[BPM To Seconds]のパラメータをすべてInput化*

Input化するとInputピンの名前が適用されます。
必要に応じて分かりやすいInput Nameを変更します。
今回は名前を変更せずに使用します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-06-48.png)
*必要に応じてInput Nameを変更する*

[BPM To Seconds]ノードを組み込んだ状態です。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-08-15.png)
*[BPM To Seconds]ノードを組み込んだ状態*

### Trigger CounterでMIDI Noteを1小節ごとにRandomに変更する

1小節ごとにMIDI Note Noをランダムに変更できるように組んでいきます。
[Input：On Play]から[Trigger Repeat]までの処理を左側に移動します。
[Trigger Repeat：RepeatOut]からドラッグ＆ドロップし、[Trigger Counter]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-10-45.png)
*[Trigger Repeat：RepeatOut]からドラッグ＆ドロップ > [Trigger Counter]を追加*

[Trigger Counter：On Reset]からドラッグ＆ドロップし、[Random(Int)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-12-45.png)
*[Trigger Counter：On Reset]からドラッグ＆ドロップ > [Random(Int)]を追加*

Random(int)のValueをMIDI Note Noとして使用するように設定します。

[**Trigger Conter**]
Reset Count：4

[**Randam(int)**]
Min：60
Max：70

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-15-31.png)
*Random(int)のValueをMIDI Note Noとして使用するように設定*

Reset Countを4にすると、5拍目が1拍目にリセットされます。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-15-57.png)
*Reset Count 4の時のTrigger Counterの動き*

MIDI Note No. 60～71はド4～シ4なので、Random (int)に60～71になる値を設定しています。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-02-19-18-56-30.png)
*MIDI Note Noの音階一覧（ド４~ド５まで）*

[Trigger Counter]ノードを組み込んだ状態です。
これで、1小節ごとにTrigger CounterのResetが実行されRandomなMIDI Note Noが再生されるようになります。

![](/images/books/ue5_metasound_createsound/chapter02_bpm_and_tempo/2022-09-28-08-16-48.png)
*[Trigger Counter]ノードを組み込んだ状態*

https://twitter.com/posita33/status/1468978903637454848
