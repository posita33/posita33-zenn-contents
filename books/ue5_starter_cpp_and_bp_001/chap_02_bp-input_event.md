---
title: "【BP】Input Event（入力イベント）"
free: false
---

## 【Blueprint】Input Event（入力イベント）

### 今回できること

キーボードやゲームコントローラーの入力イベントからPrintStringを出力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-58-18.png)

Project Settingsに入力イベントを追加して、Blueprintで追加した入力イベント呼び出します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-19-40.png)

### 学習用の新規レベル「Chapter_2_InputEvent」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-23-32.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_InputEvent」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-43-38.png)

### Blueprintを複製する

「BP_Function」を複製（Ctrl + W）して、「BP_InputEvent」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-47-04.png)

### キーボード入力イベントノードを追加する

キーボードの「H」キーを入力した時に処理を実行するようにします。

メニューから[Input > Keyboard Event > H]を選択します。
カテゴリーが英語UIと日本語UIで違うので検索Wordが変わります。

- 英語UI：[keyboard （追加したいキー）]
- 日本語UI：[キーボード （追加したいキー）]

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-10-29.png)

「H」のイベントノードの[Pressed][Released]の[実行]ピンを[PrintString]ノードとFunction[PrintCalcResult]ノードの[実行]ピンに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-49-36.png)

[Compile]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-14-10.png)

Level Editorに戻り、「BP_InputEvent」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-50-50.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[H]キーを入力してもBlueprintが反応しません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-52-48.png)

### [Enable Input]ノードを有効にしてキーボード入力できるようにする

Blueprintが入力を受け付けるように修正します。

[Sequence]ノードを追加して、[Then 0]の[実行]ピンで入力を受け付けるようにする処理を設定します。
[Enable Input]を追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-21-36.png)

[Enable Input]ノードの[Player Controller]ピンからDrag&Dropし、[Get Player Controller]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-23-14.png)

[Sequence]ノード[Then 0]の[実行]ピンを[Enable Input]ノードの[実行]ピンに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-56-25.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-14-10.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[H]キーを入力するとBlueprintが反応します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-09-58-18.png)

入力イベントノードは「Pressed（キーを押した）」「Released（キーを離した）」の入力を取得できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-00-03.png)

### Project Settingsで入力イベントを追加する

キーボードとゲームパッドのイベントを1つのイベントで処理できる設定をします。

[Project Settings]を開きます。

- [Edit]メニュー > [Project Settings...]
- 右上の[Settings] > [Project Settings...]

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-03-21.png)

入力の設定は[Engine]カテゴリーの[Input]から行います。
[Bindings]カテゴリーで詳細な入力設定を行えます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-49-03.png)
*[Engine] > [Input] > [Bindings]カテゴリー*

[Action Mappings]に「ActionPrintResult」というActionイベントを追加します。

[Action Mappings]の[+]ボタンをクリックするとActionイベントが追加されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-05-49.png)

Action Mappingsに追加されたActionを設定します。

- Action Name：ActionPrintCalcResult
- Input Key：Cキー

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-09-31.png)

Inputキーの左側のアイコンをクリックしてから、設定したいキーを入力すると設定したいキーが設定されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-11-03.png)

キーボード以外にもゲームパッドの入力を同じActionに設定できます。
Action名の[+]ボタンをクリックすることでInputキーを追加できます。

日本語UIと英語UIで名称や配置が違うので、UIを母国語にして設定した方が間違えないです。

| 日本語UI             | 英語UI                     |
| -------------------- | -------------------------- |
| ゲームパッド Aボタン | Gamepad Face Button Bottom |
| ゲームパッド Bボタン | Gamepad Face Button Right  |
| ゲームパッド Xボタン | Gamepad Face Button Left   |
| ゲームパッド Yボタン | Gamepad Face Button Top    |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-13-42.png)

### Project Settingsで追加したActionイベントを追加する

Project Settingsで追加したActionイベントを入力した時にFunction[PrintCalcResult]を処理するように修正します。

「BP_InputEvent」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-14-41.png)

メニューからProject Settingsで追加したInput Actionイベント[ActionPrintCalcResult]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-19-06-08.png)

Input Action[PrintCalcResult]の[Pressed]をFunction[PrintCalcResult]の[実行]ピンに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-17-12.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-01-27-18-14-10.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

Project Settingsで追加したActionイベントを入力した時にunction[PrintCalcResult]を処理するようになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-19-40.png)

### すべて保存する

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-input_event/2022-03-06-10-20-49.png)

## 参照URL

https://docs.unrealengine.com/4.26/ja/InteractiveExperiences/Input/SetUpInput/
