---
title: "Modulatorノードを再現する"
---

## Modulatorノードでは何ができたのか

今回はModulatorノードを再現しますがそもそもModulatorノードでは何ができたのでしょうか。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-29-47.png)
*MetaSoundでModulatorノードはどうやって再現できるのか？*

ModulartorノードではPitchとVoumeの最小（Min）～最大（Max）を設定し、その範囲内をランダムに調整できました。
Pithは「[音高（おんこう）](https://ja.wikipedia.org/wiki/%E9%9F%B3%E9%AB%98)」ともいい、数値が上がれば音が高くなり、数値が下がれば音が低くなります。
Volumeは「音量」なので、数値が上がれば音が大きくなり、数値が下がれば音が小さくなります。
Modulatorは1.0が元の音源と同じ扱いになるので、1.0より小さいか大きいかで音の聴こえ方が変わります。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-30-42.png)
*ModulatorはPith（音高）とVolume（音量）を範囲内のランダムな値で再生するノード*

MetaSoundでPitchとVolumeを特定の範囲をRandomに変更できれば、Modulatorノードを再現できます。

## 範囲内の数値でランダムにPitchを変更する

前回ランダムで再生できるようにした「MS_Explosion」をMetaSoundエディタで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-34-51.png)
*MS_Explosionを開く*

前回までの状態です。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-37-45.png)

Wave Playerに[Pitch Shift]の入力ピンがあります。[-20.0]を入力して再生すると音が少し長くなり、低くなります。[20.0]を入力して再生すると音が短くなり、高くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-40-12.png)
*PitchShiftの数値が-(マイナス)の値にすると、音が長く低くなる。0より大きくすると、音が短く高くなる*

WavePlayerのPitch Shiftを変更すればPitchを変更できました。では、特定の範囲でランダムにPitchを変更できるようにしてみましょう。
Random(Float)を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-41-10.png)
*Random(Float)を追加する*

Random(Float)をRandomGet(WaveAsset:Array)とWavePlayerの間に実行されるように設定します。
MinとMaxにPitchの最小と最大を設定します。Modulatorノードは[1.0]が元の音源でしたが、WavePlayerの[Pitch Shift]は[0.0]が元の音源になります。
変化がわかるように[-20.0～20.0]に設定します。設定できたら再生して音の高さが変わるか確認してみましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-35-31.png)
*Random(Float)でPitch Shiftをランダムに設定する*

## 範囲内の数値でランダムにVolumeを変更する

今度はVolumeを範囲内の数値でランダムに変更してみます。
WavePlayerにVolumeの設定がないので、出力した音の大きさをMixerノードで変更します。
Mixerノードを追加します。MonoとStereoがありますが、Stereoで出力するようにしているので今回は[Stereo Mixer(2)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-47-38.png)
*Stereo Mixer(2)を追加する*

Stereo Mixer(2)のIn OutをそれぞれWavePlayerのOutとOutputに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-49-59.png)

Gainの数値を変更します。
Gainの数値を小さくすると音が小さくなり、数値を大きくすると音が大きくなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-53-45.png)
*Gainの数値を変えることでボリュームの大きさを変更できる*

[【Q&A】GAINとVOLUMEの違い？](https://saimusic.jp/blog/qanda-gain-volume/)

VolumeとGainは違うもので、Outputで最終的に出力される音量がVolumeで音量になる前の音の大きさがGainみていです。

Gain 0からドラッグ＆ドラップし、[Random(Float)]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-57-22.png)
*Gain 0からRandom(Float)を追加する*

追加したRandom(Float)のMinとMaxにGain 0の範囲を設定します。
再生すると設定した範囲でVolumeがRandomに変更されて再生されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-06-59-09.png)
*Random(Float)のMinとMaxにGain 0の範囲を設定する*

[Input：On Play]と[Random(Float)：Next]を接続します。
![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-07-01-56.png)
*[Input：On Play]と[Random(Float)：Next]を接続する*

[Play]ボタンを何度かクリックして再生してみてください。
MetaSoundでもPitchとVolumeをRandomの範囲で変更でき、Modulatorノードを再現できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-07-05-36.png)

## Sound CueとMetaSoundの比較画像

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-07-06-49.png)
*Sound CueでModulatorノードを使用した処理*

![](/images/books/ue5_starter_cpp_and_bp_001/chapter01_modulator/2022-02-18-07-07-57.png)
*MetaSoundでModulatorノードを使用した時と同様の処理*
