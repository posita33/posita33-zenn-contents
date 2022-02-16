---
title: "(修正中)Randomに再生する"
---

## Randomに再生する

[MS_Explosion]に[Explosion01]と[Explosion02]をランダムに再生できるように編集します。
[MS_Explosion]をMetaSoundエディタで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-22-52-10.png)
*MS_Explosionを開きます*

MS_Explosionを開きます
randomでノード検索を行い、[Random Get(WaveAsset:Array)]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-22-53-19.png)
*Random Get(WaveAsset:Array)を選択*

[In Array]ピンからドラッグ＆ドロップして、[Promote To Graph Input]を作成します。Blueprintでピンから変数を作成する時と同様のことを行います。ピンから作成すると変数の型を設定した状態で変数を作成できるので便利です。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-22-53-34.png)
*In Arrayからドラッグ＆ドロップ > Promote To Graph Inputを選択*

Defaultの項目の[+]を2回クリックして配列を2つ追加します。
Index[0]に[Explosion01]、Index[1]に[Explosion02]を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-22-57-50.png)
*配列を２つ追加し、Index[0]:[Explosion01]とIndex[1]:[Explosion02]を設定する*

[Random Get(WaveAsset:Array)]を[Input:On Play]と[Wave Player]の中間で実行されるようにピンを繋ぎ直します。
・[Input: On Play] と [Random Get(WaveAsset:Array)の Next]
・[Random Get(WaveAsset:Array) On Next]と[Wave PlayerのPlay]
・[Random Get(WaveAsset:Array) Value]と[Wave PlayerのWave Asset]

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-22-55-29.png)
*Random Get（WaveAsset:Array）が実行されるようにピンを繋ぎ直す*

PlayをクリックするとSoundsに設定したSoundWaveがRandomに再生されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-22-55-55.png)
*Playを何度かクリックするとRandomにSoundWaveが再生される*

[Explosion01]と[Explosion02]の音が似ているので、Index[01]を[Floating_UI_Open]に設定して再生します。
全然違う音源をランダムに再生することでランダムに再生されているか確認しやすくなります。
![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-23-01-11.png)
*似ていない音源を再生するようにしてランダム再生を確認する*

ランダムに再生することが確認出来たら、Soundsの設定を元に戻します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-23-01-52.png)
*配列を２つ追加し、Index[0]:[Explosion01]とIndex[1]:[Explosion02]を設定する*

SoundCueと比較するとMetaSoundは変数を使えるBlueprintに似ています。
MetaSoundを触るのであればBlueprintの変数定義について学習しておくことをお勧めします。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-23-02-19.png)
*SoundCueのRandom再生する処理*

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_random/2022-02-16-23-02-35.png)
*MetaSoundのRandom再生する処理*

