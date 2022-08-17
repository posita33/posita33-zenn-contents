---
title: "Modulatorノードを再現する"
---

## Modulatorノードでは何ができたのか

今回はModulatorノードを再現しますがそもそもModulatorノードでは何ができたのでしょうか。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-02-18-06-29-47.png)
*MetaSoundでModulatorノードはどうやって再現できるのか？*

ModulartorノードではPitchとVoumeの最小（Min）～最大（Max）を設定し、その範囲内をランダムに調整できました。
Pithは「[音高（おんこう）](https://ja.wikipedia.org/wiki/%E9%9F%B3%E9%AB%98)」ともいい、数値が上がれば音が高くなり、数値が下がれば音が低くなります。
Volumeは「音量」なので、数値が上がれば音が大きくなり、数値が下がれば音が小さくなります。
Modulatorは1.0が元の音源と同じ扱いになるので、1.0より小さいか大きいかで音の聴こえ方が変わります。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-02-18-06-30-42.png)
*ModulatorはPith（音高）とVolume（音量）を範囲内のランダムな値で再生するノード*

MetaSoundでPitchとVolumeを特定の範囲をRandomに変更できれば、Modulatorノードを再現できます。

## 範囲内の数値でランダムにPitchを変更する

前回ランダムで再生できるようにした「MS_Explosion」をMetaSoundエディタで開きます。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-17-07-32-26.png)
*MS_Explosionを開く*

前回までの状態です。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-01-05.png)

Wave Playerに[Pitch Shift]の入力ピンがあります。[-20.0]を入力して再生すると音が少し長くなり、低くなります。[20.0]を入力して再生すると音が短くなり、高くなります。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-02-23.png)
*PitchShiftの数値が-(マイナス)の値にすると、音が長く低くなる。0より大きくすると、音が短く高くなる*

WavePlayerのPitch Shiftを変更すればPitchを変更できました。では、特定の範囲でランダムにPitchを変更できるようにしてみましょう。
[Random(Float)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-03-49.png)
*Random(Float)を追加する*

Random(Float)をRandomGet(WaveAsset:Array)とWavePlayerの間に実行されるように設定します。
MinとMaxにPitchの最小と最大を設定します。Modulatorノードは[1.0]が元の音源でしたが、WavePlayerの[Pitch Shift]は[0.0]が元の音源になります。
変化がわかるように[-20.0～20.0]に設定します。設定できたら再生して音の高さが変わるか確認してみましょう。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-06-25.png)
*Random(Float)でPitch Shiftをランダムに設定する*

## 範囲内の数値でランダムにVolumeを変更する

今度はVolumeを範囲内の数値でランダムに変更してみます。
WavePlayerにVolumeの設定がないので、出力した音の大きさをMixerノードで変更します。
Mixerノードを追加します。MonoとStereoがありますが、Stereoで出力するようにしているので今回は[Stereo Mixer(2)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-08-16.png)
*Stereo Mixer(2)を追加する*

Stereo Mixer(2)のIn OutをそれぞれWavePlayerのOutとOutputに接続します。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-09-57.png)

Gainの数値を変更します。
Gainの数値を小さくすると音が小さくなり、数値を大きくすると音が大きくなります。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-14-21.png)
*Gainの数値を変えることでボリュームの大きさを変更できる*

[【Q&A】GAINとVOLUMEの違い？](https://saimusic.jp/blog/qanda-gain-volume/)

VolumeとGainは違うもので、Outputで最終的に出力される音量がVolumeで音量になる前の音の大きさがGainみていです。

Gain 0からドラッグ＆ドラップし、[Random(Float)]を追加します。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-15-45.png)
*Gain 0からRandom(Float)を追加する*

追加したRandom(Float)のMinとMaxに範囲を設定します。
Gain 1(Lin)にもRandom(Float):Valueを接続します。
再生すると設定した範囲でVolumeがRandomに変更されて再生されます。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-18-10.png)
*Random(Float)のMinとMaxに範囲を設定する*

[Input：On Play]と[Random(Float)：Next]を接続します。
![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-20-44.png)
*[Input：On Play]と[Random(Float)：Next]を接続する*

[Play]ボタンを何度かクリックして再生してみてください。
MetaSoundでもPitchとVolumeをRandomの範囲で変更でき、Modulatorノードを再現できました。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-23-49.png)

## Sound CueとMetaSoundの比較画像

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-02-18-07-06-49.png)
*Sound CueでModulatorノードを使用した処理*

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-24-38.png)
*MetaSoundでModulatorノードを使用した時と同様の処理*

## Multiply(Audio by float)でGainを変更する方法

Output Formatを[Mono]に変更します。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-26-58.png)

AudioピンからDrag&Dropし、[multiply(Audio by Float)]を選択します。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-28-56.png)

Float側に[Random(Float):Value]を接続するとAudioのGainを変更できます。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-29-57.png)

モノラルの音源であれば、[Multiply(Audio by float)]ノードでGainを調整する方が簡単です。

![](/images/books/ue5_metasound_createsound/chapter01_modulator/2022-08-18-08-30-43.png)
