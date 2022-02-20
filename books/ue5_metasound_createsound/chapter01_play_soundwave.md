---
title: "音源（Sound Wave）を再生する"
---

## Porojectを作成する

UE5でStarterContentsを含むプロジェクトを作成します。

UE5を起動します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-21-53-28.png)

プロジェクトを作成します。

| プロパティ      | 設定        |
| --------------- | ----------- |
| カテゴリ        | Games       |
| テンプレート    | ThirdPerson |
| C++ or BP       | BP          |
| StarterContents | あり        |
| プロジェクト名  | MetaSound   |

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-21-53-43.png)

## MetaSoundプラグインを有効にする

プロジェクトを作成したら、MetaSoundプラグインを有効にしましょう。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-02-37.png)
*[Edit] > [Plugins]*

MetaSoundプラグインを有効にします。
[MetaSound]で検索 > Enabledをクリック > Beta版だけど使用するかを確認するダイアログが表示されるので[Yes]をクリック > [Restart Now]をクリックするとプロジェクトが再起動され、MetaSoundが有効になります。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-04-36.png)

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-05-18.png)

プロジェクトが立ち上がるとコンテンツブラウザから新規作成の項目で [Sounds]のカテゴリから[MetaSound]が選択できるようになります。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-06-46.png)

## Sound WaveをMetaSoundで再生する

それでは、MetaSoundでSoundWaveアセットを再生してみましょう。

SoundWaveアセットはStarterContent > Audioフォルダにサンプルとしていくつか用意されています。今回はこの中の[Explosion01]をMetaSoundで再生してみます。 
UE5はサムネイルのサイズが大きいので、Settings > Thumbnail Size > Smallを選択するとサムネイルが見やすくなります。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-09-24.png)

フォルダを作成します。
```
Content/
  └ MetaSound/
     └ Audio/
```

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-16-06.png)

AudioフォルダにMetaSound[MS_Explosion]を作成します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-21-38.png)

MS_ExplosionをダブルクリックしてMetaSoundエディタ開きます。
ブループリントを編集するエディタと似ています。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-09-49.png)

サウンドキューの感覚でSoundWaveアセットをMetaSoundグラフにドラッグ&ドロップしてもノードが追加されません。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-10-00.png)

WavePlayerノードを追加し、Wave Assetに[Explosion01]を設定します。
Input：On PlayとWave PlayerのPlayピンを接続します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-10-13.png)

Wave PlayerのOut Leftピンと Output: Audioピンを接続します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-10-35.png)

[Play]ボタンを押すと[Explosion01]が再生されます。
右側のメーターも再生に応じて変化します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-10-46.png)

## ステレオ出力に変換する

Wave Playerのオーディオ出力がステレオ出力なのに対して、MetaSoundのオーディオ出力がデフォルトのモノラル出力になっています。MetaSoundのオーディオ出力をステレオ出力に変換してWavePlayerのオーディオ出力に合わせます。

ツールバーの[MetaSound]をクリック > Output Formatを[Stereo]に変更します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-11-08.png)

Wave Playerとオーディオ出力がステレオ出力になったことで、音源の左右の聴こえ方を再現できるようになりました。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-11-17.png)

## Output [On Finished]を呼び出して終了する

MetaSoundはPlayボタンを押してから、音が流れなくなっても再生を続けます。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-38-10.png)

[Stop]ボタンをクリックするとタイムやノードのパルスが停止します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-39-59.png)

[Wave Playerノード：On Finished]と[Output：On inisehed]を接続します。
[Wave Playerノード：On Finished]はSound Waveの再生が終了した時に実行されます。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-40-54.png)

[Play]ボタンをクリックし、Sound Waveの再生が終わると、[Output：On inisehed]が呼ばれます。
[Output：On inisehed]は[Stop]ボタンをクリックした時と同様にタイムやノードのパルスが停止します。

![](/images/books/ue5_metasound_createsound/chapter01_play_soundwave/2022-02-16-22-42-17.png)

