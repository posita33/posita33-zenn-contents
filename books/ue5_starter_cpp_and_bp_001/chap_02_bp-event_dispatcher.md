---
title: "【BP】Event Dispatcher"
free: false
---

## 【Blueprint】Event Dispatcher

### 今回できること

Event Dispatcherを作成します。
作成したEvent DispatcherにCustom EventをBindします。
「H」キーをPressした時に、Event Dispatherを呼び出し、Custom Eventを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-13-14.png)

### 学習用の新規レベル「Chapter_2_EventDispatcher」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-03-09-06-14-25.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_EventDispather」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-10-50-33.png)

### Blueprintを複製する

「BP_InputEvent」を複製（Ctrl + D）して、「BP_EventDispatcher」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-10-53-01.png)

### Event Dispatcher[OnPrintHello]を追加する

Event Dispatcher[OnPrintHello]を作成します。

「BP_EventDispatcher」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-10-57-09.png)

[My Blueprint]パネルの[Event Dispatchers]カテゴリーの[+]ボタンをクリックします。
追加されたEvent Dispatherの名前を[OnPrintHello]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-00-18.png)

### Event Dispatcher[OnPrintHello]をCustom Event[PrintHello]にバインドする

Event Dispatcher[OnPrintHello]をEvent GraphにDrag&Dropします。
メニューから[Bind]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-01-28-15-16-25.png)

「Bind Event to On Print Hello」と書かれたノードのEvent（赤い四角）からDrag&Dropします。
メニューから[Add Custom Event...]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-01-28-15-26-11.png)

追加したCustom Eventの名前を[PrintHello]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-01-28-15-28-01.png)

Custom Event[PrintHello]の[実行]ピンを”Hello World!”を出力するPrintStringに接続します。
「H」キーのPressedの接続を切ります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-03-08.png)

### 「H」キーのPressedからEventDispatcher「OnPrintHello」を呼び出す

Event Dispatcher[OnPrintHello]をEvent GraphにDrag&Dropします。
メニューから[Call]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-04-52.png)

「H」キーのPressedとEvent Dispatcher[OnPrintHello]のCallノードを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-06-33.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-01-28-15-35-46.png)

Level Editorに戻り、「BP_EventDispatcher」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-07-46.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

「H」キーをPressすると、Event Dispatcher[OnPrintHello]のCallノードが呼ばれた後に、Custom Event[PrintHello]が呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-10-19.png)

Event DispatherにBindしたイベントは、Event Dispatherを呼び出す（Call）と、Bindしたイベントが呼ばれます。
イベントを呼ぶことがTrrigerとなるので、Tickイベントで監視するような処理を書くより処理が軽くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-13-14.png)

### すべて保存する

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-03-06-11-14-21.png)

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/EventDispatcher/
