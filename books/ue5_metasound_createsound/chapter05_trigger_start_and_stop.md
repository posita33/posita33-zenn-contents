---
title: "BlueprintでTriggerのPlayとStopを制御する"
---

:::message
TODO: 手順をBook用に最適化中
:::

## WavePlayerのPlayとStopを制御するTriggerを追加する

前回サウンドの減衰を確認するために配置したMetaSound[MS_Explosion1]を再生/停止できるように変更します。
まずは[MS_Explosion1]をMetaSoundエディタで開きます。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-05-45.png)
*前回のサウンドの減衰を確認するために配置したMetaSound[MS_Explosion1]を再利用*

MetaSoundパネルの[INPUTS]の右側にある[+]をクリックして新しいInputを追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-06-04.png)
*新しいInputを追加する*

[Inspector]パネルの[Input Name]と[Type]を変更します。

- Input Name : On Stop
- Type：Trigger 

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-06-28.png)
*Input NameとTypeを変更する*

グラフ内で右クリックし、リストから[Get On Stop]を選択してInputで追加したTriggerを追加します。
ブループリント感覚でドラッグ＆ドロップの追加を試みましたが出来ませんでした。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-06-46.png)
*右クリック > [Get On Stop]*

[Input：On Stop]と[Wave PlayerのStop]を接続します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-06-58.png)
*[Input Stop]と[Wave PlayerのStop]を接続*

[Play]ボタンをクリックすると[Explosion01]がループ再生されます。
再生された後に、[Input：On Stop]を選択し、[Inspector]パネル [Simulate]の[↓]をクリックします。（Input ノードの右上の[↓]ボタンをクリックしても同じように実行されます）
[Input : On Stop]が[WavePlayer]の[Stop]を呼び出して音源の再生を停止させます。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-07-17.png)
*Playボタンを押した後に、[On Stop]をSimulateボタンで呼び出すとWavePlayerの再生が停止する*

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-07-29.png)
*Inputノードの右上の[↓]ボタンをクリックでもSimulateボタンを押したことになる*

[Input : On Play]のSimulateボタンを押せば再び再生できるのかと思いましたが、SpectorタブにSimulateボタンがありませんでした。
[Input：On Play]は[Play]ボタンを押した時の起点となる特殊なノードという扱いのようです。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-07-45.png)
*Input : On Playは[Play]ボタンを押した時のみ実行される*

新しいInputのTriggerを追加します。

- Input Name：On PlayStart
- Type：Trigger

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-08-36.png)
*新しいInputのTrigger：On PlayStartを追加する*

[Get On PlayStart]を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-08-52.png)
*[Get On PlayStart]を追加する*

[Input : On PlayStart]と[Wave Player : Play]を接続します。
Blueprintの実行ピンでは複数実行ピンを接続できましたが、Triggerのノードは1つのピンしか接続できません。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-09-20.png)
*[Input : On PlayStart]と[Wave Player : Play]を接続*

[Play]ボタンを押してから、[On PlayStart]の[↓]ボタンを押すと[Wave PlayerのPlay]が実行されます。Wave PlayerがPlayの状態の時に、[On Stop]の[↓]ボタンを押すと[Wave PlayerのStop]が実行されて停止します。[On PlayStart]の[↓]ボタンを押せばWavePlayerが再び再生されるので、Triggerで再生と停止を制御することが出来ます。
[Play]ボタンを押す前に[On PlayStart]の[↓]ボタンを押しても[Wave PlayerのPlay]は実行されません。Triggerは[Play]ボタンを押した時にのみ実行されます。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-09-38.png)
*Triggerノードの[On PlayStart]と[On Stop]で再生と停止を制御出来るようになる*

## ブループリントでTrigger[On PlayStart]と[On Stop]を呼び出す

特定な領域（Trigger Volume）に入った時に[On PlayStart]を呼び出して停止し、範囲から出たら[On Stop]を呼び出して再生させるようにします。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-10-04.png)
*特定のエリアに入ったら[On PlayStart]で再生、エリアを出たら[On Stop]で停止*

#### TriggerVolumeとPlaneを配置する

[Trigger Volume]をViewportに追加します

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-10-25.png)
*TriggerVolumeを追加する：Create > Volume > Trigger Volume*

Trigger Volumeの大きさを調整します(Brush Shapeプロパティでエリアの範囲を調整する)。
Playをしてからエリアが分からないのでPlaneを配置して、エリアが分かるように可視化します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-10-38.png)
*Trigger Volumeのエリア範囲を調整し、Planeでエリアを可視化する*

#### TriggerVolume内に入った時(OnActorBeginOverlap)に[On PlayStart]を実行する

TriggerVolumeに入った時にイベントを発生するように[OnActorBeginOverlap]を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-10-58.png)
*TriggerVolumeを右クリック > Add Event > OnActorBeginOverlap*

Level Blueprintが開きます。
ビューポートの[MS_Explosion1]を選択して、Level Blueprintに[MS_Explosion1]の参照を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-11-24.png)
*ビューポートの[MS_Explosion1]を選択 > イベントグラフを右クリック > Create a Reference to MS_Explosion1*

MS_Explosion1の参照から[Get Parameter Interface(AudioComponent)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-11-51.png)
*MS_Explosion1の参照からドラッグ＆ドロップ > Get Parameter Interface(AudioComponent)*

[Get Parameter Interface]から[Trigger(Interface Call)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-12-04.png)
*Get Parameter Interface > Trigger(Interface Call)*

実行ピンを接続してOnActorBeginOverlapが発生した際にTriggerノードが実行されるようにします。
TriggerノードのNameには[On PlayerStart]を設定します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-12-24.png)
*実行ピンを接続し、TriggerノードのNameに[On PlayStart]を設定する*

PlayしてTriggerVolume内に入ると音源が再生されます。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-12-45.png)
*エリア内に入ると音源が再生されます*

Triggerノードが実行された時に、MetaSound側に同じ名前のインプットがあった時にはInputが実行されます。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-13-05.png)
*Triggerノードで指定した名前のInputが実行される*

#### TriggerVolume内から出た時(OnActorEndOverlap)に[On Stop]を実行する

次はエリアから出た時に[On Stop]が呼ばれるように実装していきます。
TriggerVolumeから出た時にイベントを発生するように[OnActorEndOverlap]を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-13-23.png)
*TriggerVolumeを右クリック > Add Event > OnActorEndOverlap*

[Get Parameter Interface]から[Trigger(Interface Call)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-13-34.png)
*Get Parameter Interface > Trigger(Interface Call)*

実行ピンを接続してOnActorEndOverlapが発生した際にTriggerノードが実行されるようにします。
TriggerノードのNameには[On Stop]を設定します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-14-00.png)
*実行ピンを接続し、TriggerノードのNameに[On Stop]を設定する*

Playしてから一度エリア内に入り音源が再生されて、エリア外に出ると音源が停止します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-14-17.png)
*エリアの外に出ると音源が停止する*

これでエリア内に入ると[On PlayStart]が実行され音源が再生され、エリア外に出ると[On Stop]が実行され音源が停止するようになります。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-14-30.png)
*ブループリントでMetaSoundのTriggerを制御して再生と停止を行う*

### ブループリントでTriggerを使わずに再生/停止する

Triggerを使用しないで音源を再生するにはどうしたらいいでしょうか。
[OnPlay]で再生して、音源を停止する方法について試してみます。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-14-48.png)
*On Playで再生する処理*

LevelBlueprintを開きます。
Audio ComponentからPlayを呼び出すようにします。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-15-01.png)
*Audio ComponentからStartを呼び出す*

Audio ComponentからStopを呼び出すようにします。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-15-12.png)
*Audio ComponentからStopを呼び出す*

実行ピンを接続します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-15-23.png)
*実行ピンを接続する*

Event BeginPlayを追加します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-15-45.png)
*Event BeginPlayを追加する*

Event BeginPlayはPlayした時に実行されるので、プレイしたら音源を停止した状態にし、エリアに入ったら音源が再生されるようにします。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-15-58.png)
*Event BeginPlayが呼ばれたらStopを呼び出す*

Playしてエリアに入ると音源が再生され、エリアから出ると音源が停止します。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-16-09.png)
*エリアに入ると音源が再生され、エリアから出ると音源が停止する*

Triggerを使わない方法はツールバーの[Play]ボタンと[Stop]ボタンを押すような動きをします。

![](/images/books/ue5_metasound_createsound/chapter05_trigger_start_and_stop/2022-02-20-22-16-22.png)
*ツールバーの[Play][Stop]ボタンを押すような動きをする*
