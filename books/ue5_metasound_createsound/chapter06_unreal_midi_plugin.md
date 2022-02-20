---
title: "MidiファイルでMetaSoundを演奏させる（Unreal-Midiプラグイン）"
---

:::message
TODO: 手順をBook用に最適化中
:::

初めに今回実装する内容について
MetaSoundはMIDI Note Noで音を再生することが出来ます。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-23-56.png)
*MetaSoundはMIDI Noteを指定して音を再生することが出来る*

MIDIファイルをUE5で扱うことが出来れば、MIDIファイルを使って音楽を再生できます。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-24-30.png)
*MIDIファイルはMIDI Note Noの演奏データ*

https://ja.wikipedia.org/wiki/%E3%82%B9%E3%82%BF%E3%83%B3%E3%83%80%E3%83%BC%E3%83%89MIDI%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB

Unreal EngineでMIDIファイルを扱うことが出来るプラグイン「Midi-Unreal」がGithubに公開されているので、UE5 EAで使用出来るようにします。

https://github.com/Geromatic/Midi-Unreal/

## Midi-UnrealをUE5 EAで使用できるようにする

UE5 EAでC++のBlankプロジェクトを作成します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-25-14.png)
*UE5 EAでC++のBlankプロジェクトを作成する*

Midi-UnrealをZipファイルでダウンロードします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-25-29.png)
*Midi-UnrealをZipファイルでダウンロードする*

https://github.com/Geromatic/Midi-Unreal/

ダウンロードしたMidi-UnrealのZipファイルを展開します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-25-54.png)
*ダウンロードしたMidi-UnrealのZipファイルを展開する*

プロジェクトフォルダに「Plugins」を作成して、Midi-UnrealのZipファイルを展開したフォルダ内の「MidiAsset」フォルダをコピーします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-26-05.png)
*「MidiAsset」フォルダを「Plugins」フォルダにコピーする*

UE5のプロジェクトを閉じます。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-26-18.png)
*プロジェクトを閉じる*

uprojectファイルを右クリックし、[Generate Visual Studio project files]を実行します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-26-29.png)
*uprojectファイルを右クリック > [Generate Visual Studio project files]*

[5.0]を選択して、[OK]をクリックします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-26-45.png)
*[5.0]を選択 > [OK]をクリック*

エラー内容が表示されます。
UE5がWin32に対応していないので、Build.csがエラーになっています。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-27-01.png)
*エラーが表示（UE5はWin32に対応していない）*

エラーになっているBuild.csのWin32を判定している処理を削除します。

```csharp:MidiInterface.Build.cs
	// Windows
	if (Target.Platform == UnrealTargetPlatform.Win32 || Target.Platform == UnrealTargetPlatform.Win64)
	{
		PublicDefinitions.Add("__STDC_WANT_SECURE_LIB__=1"); // ignore warning
		PublicDefinitions.Add("__WINDOWS_MM__=1");
		PublicAdditionalLibraries.Add("winmm.lib");
	}
↓
	// Windows
	if (Target.Platform == UnrealTargetPlatform.Win64)
		PublicDefinitions.Add("__STDC_WANT_SECURE_LIB__=1"); // ignore warning
		PublicDefinitions.Add("__WINDOWS_MM__=1");
		PublicAdditionalLibraries.Add("winmm.lib");
	}
```

```csharp:ProceduralAudio.Build.cs
	// Windows
	if (Target.Platform == UnrealTargetPlatform.Win32 || Target.Platform == UnrealTargetPlatform.Win64)
	{
		PublicDefinitions.Add("__STDC_WANT_SECURE_LIB__=1"); // ignore warning
	}
↓
	// Windows
	if (Target.Platform == UnrealTargetPlatform.Win64)
	{
		PublicDefinitions.Add("__STDC_WANT_SECURE_LIB__=1"); // ignore warning
	}
```

再び[Generate Visual Studio project files]を実行します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-28-04.png)
*再び[Generate Visual Studio project files]を実行*

今度はGenerateに成功したので、プロジェクトを再度開きます。
プラグインを再ビルドするようにダイアログが表示されるので[OK]をクリックします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-28-15.png)
*プロジェクトを開くと、プラグインを再ビルドする*

プロジェクトが開かれると、MidiAssetがプラグインフォルダに追加されています。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-28-27.png)
*MidiAssetがプラグインフォルダに追加される*

Midiファイルをコンテンツブラウザにドラッグ＆ドロップします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-28-50.png)
*Midiファイルをコンテンツブラウザにドラッグ＆ドロップ*

MIDIファイルがUE5のアセットとして追加することが出来るようになりました。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-29-03.png)
*UE5でMIDIファイルが追加できるようになった*

## MIDI Noteと音の大きさを変更できるMetaSoundを作成する

MetaSoundプラグインを有効にして、MetaSound「MT_Neko」を作成します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-29-46.png)
*コンテンツブラウザを右クリック > Sounds > MetaSound > MT_Neko*

MIDI NoteとGain(音の大きさ)を変更できるMetaSoundを作成します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-30-01.png)
*MIDI NoteとGain(音の大きさ)を変更できるMetaSoundを作成*

## MIDIファイルをMetaSoundで再生するブループリントを作成する

### MIDIファイルを再生する処理を実装する

Actorを親とするブループリント[BP_PlayMIDI]を作成します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-30-25.png)
*コンテンツブラウザを右クリック > Blueprint Class > Actor > BP_PlayMIDI*

コンポーネントに[MIDI Processor Component]を追加します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-30-38.png)
*コンポーネント ADD > MIDI Processor Component*

MidiファイルのStartとStopイベントをバインドする処理を追加します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-30-50.png)
*MidiファイルのStartとStopイベントをバインドする処理を追加*

Midiファイルのノートが処理された時に実行されるイベントをバインドする処理を実装します。
イベントをバインドした際に取得できるEvent情報を分解して、各ピンがどんな情報を出力するのかPrintStringで出力するようにします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-31-01.png)
*Midiファイルのノートが処理された時に実行されるイベントをバインドする処理を実装*

Midiファイルを読み込んで再生する処理を実装します。
Midi Assetにはプロジェクトに追加したMidiファイルを設定します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-31-12.png)
*Midiファイルを読み込んで再生する処理を実装*

Midiファイルを扱うための処理の全体図になります。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-31-28.png)
*Midiファイルを扱うための処理の全体図*

ブループリントをビューポートに追加して、[Play]ボタンをクリックします。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-31-44.png)
*ブループリントをビューポートに追加 > Playボタンをクリック*

PrintStringの出力結果を元に、MidiEventの各ピンが何を出力するのか確認します。
Type：Note Off, Note On
Channel：1, 2
Data1：MIDI Note No
Data2：Volume(0～100)

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-32-04.png)
*PrintStringの出力結果を元に、MidiEventの各ピンが何を出力するのか確認する*

### MetaSoundのMIDI NoteとGain（音の大きさ）を変更する処理を実装する

MIDIファイルが2チャンネル持っているので、チャンネルごとに再生するようにMetaSoundをコンポーネントに２つ追加します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-32-27.png)
*チャンネルごとに再生するようにMetaSoundをコンポーネントに2つ追加する*
名前をChannelが分かるような名前に変更します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-32-42.png)
*名前をChannelが分かるような名前に変更する*

まずはChannel1を再生する処理を実装します。
Gainは[0.0～1.0]に対して、Data2は[0～100]なので、Data2を100で割った数をGainに設定します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-32-52.png)
*Channel1を再生する処理*

MIDIファイルのStart,StopでMetaSoundをPlay,Stopする処理を実装します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-33-03.png)
*MIDIファイルのStart,StopでMetaSoundをPlay,Stopする処理*

この状態で[Play]をクリックすると1chのみ再生されます。
2chを再生する処理実装する前に、1chのMIDI Event処理を関数化します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-33-15.png)
*1chのMIDI Event処理を関数化する*

関数名とInputのパラメータを分かりやすい名前に変更します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-33-26.png)
*関数名とInputのパラメータを分かりやすい名前に変更する*

MIDI Eventの処理を関数化できました。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-34-08.png)
*MIDI Eventの処理を関数化*

2chのMetaSoundを再生するように実装します。
関数化したことによって処理がシンプルになりました。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-34-26.png)
*2chのMetaSoundを再生するように実装する*

2ch用のMetaSoundもPlay,Stopするように実装します。

![](/images/books/ue5_metasound_createsound/chapter06_unreal_midi_plugin/2022-02-20-22-34-41.png)
*2ch用のMetaSoundもPlay,Stopするように実装する*

この状態でPlayをクリックするとMIDIファイルをMetaSoundで演奏できるようになりました。

https://twitter.com/posita33/status/1475704433388699649
