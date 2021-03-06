---
title: "【BP】PrintStringでHello World!"
free: false
---

## 【Blueprint】PrintStringでHello World!

### 今回できること

[PrintString]ノードでViewportやOutputLogに文字列を出力できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-10-07-22.png)

Blueprintのコメントの書くことができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-48-12.png)

### Mapsフォルダを作成してレベルを保存する

学習用のレベルとして保存します。
「Maps」フォルダを作為します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-08-53-12.png)

[File]メニューから[New Level...]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-08-55-13.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-03-09-06-14-25.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-08-57-40.png)

「Maps」フォルダを選択し、Nameに[Chapter_2_HelloWorld]という名称で保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-08-59-12.png)

### Blueprint Editorについて

Class Blueprint「BP_HelloWorld」をダブルクリックし、Blueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-00-19.png)

Blueprint Editorが開きます。

ときどき、データ専用ブループリントが立ち上がることもあります。

https://docs.unrealengine.com/4.26/ja/ProgrammingAndScripting/Blueprints/UserGuide/Types/ClassBlueprint/#%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E3%81%BF%E3%81%AE%E3%83%96%E3%83%AB%E3%83%BC%E3%83%97%E3%83%AA%E3%83%B3%E3%83%88

「Hello World!」を出力する処理を書くので、データ専用ブループリントが立ち上がった時は「Open Full Blueprint Editor」をクリックしてください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-08-06-11-53.png)

編集できるBlueprint Editorが開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-01-38.png)

Actor ClassのBlueprintには3種類のタブが用意されています。

- **Viewport**：コンポーネントを設定します。
- **Construction Script**：レベルのViewportに配置した後、プロパティを変更する処理を実装します。
- **Event Graph**：ブループリントの処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-34-54.png)

今回は**Event Graph**に処理を実装します。
1つ1つのメニューやボタンについては、公式ドキュメントを参照してください。

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/Editor/UIBreakdowns/ClassBPUI/

### Event BeginPlayにPrint Stringを実行する処理を実装する

Print Stringノードを実行して、プレイした時にLevelEditorのViewportに文字を出力する処理を実装します。
まずはPrint Stringノードを追加します。
次の手順はノードを追加する時の基本的な手順です。

1. EventGraphを選択します。
2. EventGraphの空きスペースを右クリックします。
3. メニューの検索バーに[print string]と入力して検索します。
4. メニューから[Print String]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-05-22.png)

1. Event BeginPlayからPrintStringを実行するように実装します。
BeginPlayイベントノードは[Play]ボタンをクリックした時に実行されるイベントです。
Event BeginPlayの実行ピンとPrintStringの実行ピンを接続します。
実行ピンは野球のホームベースを横にしたようなアイコンです。
マウスを左クリックし、ドラッグ&ドロップすることで接続できます。
2. Print StringのIn Stringに「Hello World!」と設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-08-01.png)

処理が実行されるかどうか確認します。
その前に、ノードを変更して確認したい時は左上の[Compile]ボタンをクリックして、[Save]ボタンをクリックするようにしてください。
[Compie]ボタンをクリックすると、エラーかどうか分かったり、Blueprintの変更が反映されます。[Compile]ボタンをクリックしないと正しい結果を確認できないことがあります。

**プレイして確認する前には必ず[Compile]ボタンをクリックする癖をつけましょう。**

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-09-33.png)
*プレイして確認する前に、変更したら[Compile]ボタンをクリック > [Save]ボタンをクリック*

### LevelEditorのViewportにBlueprintを追加してプレイする

ViewportにBlueprintを配置する前に[Place Actors]パネルを表示しましょう。
[Window]メニューから[Place Actors]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-12-45.png)

[Place Actors]タブを[Content Drawer]と同じように、折りたためるようにします。
タブを折りたためる機能はUE5から搭載されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-16-18.png)
*タブを右クリック > Move To Sidebar*

「BP_HelloWorld」をLevelEditorのViewportに追加します。
追加する方法は2つあります。

- [Content Browser],[Content Drawer]から「BP_HelloWorld」をViewportにDrag&Drop
- [Place Actors]の検索バーで「BP_HelloWorld」を検索して、ViewportにDrag&Drop

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-44-18.png)
*Content Browser,Content DrawerかPlace Actorsから、レベルのビューポートにDrag&Drop*

「Play」ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

Level EditorのViewport左上に「Print String」ノードの[In String]に設定した文字列の「Hello World!」が表示されます。
キーボードの[ESC]キーで終了します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-46-01.png)

### PrintStringノードの隠された設定について

「BP_HelloWorld」をダブルクリックし、Blueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-00-19.png)
*BP_HelloWorldをダブルクリック*

Print Stringノードの[Development Only]にある▽ボタンをクリックします。
Print Stringの左側に隠されていた入力ピンが表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-41-44.png)

Text Colorの右側の水色をクリックすると[Color Picker]ダイアログが表示されます。[Color Picker]から別の色を選択して、[OK]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-41-57.png)

Text Colorの右側の色が[Color Picker]で選択色に変わりました。
Durationの入力値を[10.0]に変更します。
Durationは表示時間を設定できます。[1.0]の時に1秒表示するので、[10.0]を設定すると10秒間表示するようになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-42-14.png)

英単語が分からない時に、「英単語　意味」で検索すると何をしてくれるピンなのか分かります。
最近ではGoogle ChromeのURLに文字を入力するだけで日本語の訳が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-42-26.png)

ノードを変更したので、忘れずに[Compile] > [Save]します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-09-33.png)

Level Editor側に戻って、[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

Level EditorのViewport左上に表示される文字列が10秒間表示されます。
文字列の色もColor Pickerで設定した色に表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-49-04.png)

[Window]メニューから[Output Log]タブを表示します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-54-24.png)
*Window > OutputLog*

[Content Drawer]右隣の[Output Log]タブをクリックすることで表示できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-55-45.png)

一番下までスクロールすると[Print String]の[In String]で設定した文字列が出力されています。

```
LogBlueprintUserMessages: [BP_HelloWorld_C_2] Hello World!
```

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-57-40.png)

Print Stringは2個所にIn Stringで設定した文字列を出力できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-10-07-22.png)

[Print String]の[Print to Screen]、[Print to Log]のチェックボックスを無効にすると、[In String]の文字列が出力されなくなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-10-10-46.png)

Print Stringノードはまた使用するので、確認が済んだらチェックボックスを有効に戻しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-46-14.png)

### Blueprintのコメント

Blueprintにコメントを書きます。
コメントは処理を読む人のヒントになります。自分自身でも久しぶりに読む処理は分からないこともあるので、未来の自分に当てたヒントにもなります。

コメントは次の**2種類**あります。

- ノードコメント
- コメントボックス

### ノードコメントを入力する

**ノードコメント**はノード1つに対してコメントします。
ノードを右クリックし、Node Commentのテキストボックスにコメントを入力します。
ノードコメントを入力するとノードの右上にコメントが表示されます。

**ノードが何をしているのか伝えるのに重宝します。**

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-47-25.png)

### コメントボックスを追加する

**コメントボックス**は複数ノードのコメントに重宝します。1つのノードにもコメントボックスは追加できます。

複数のノードを選択したら、キーボードの「C」キーを入力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-47-51.png)

文字列部分にコメント入力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-48-02.png)

詳細パネルからさらにコメントボックスの色やフォントサイズの設定を変更できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-48-12.png)

[Show Bubble When Zoomed]を有効にすると、ズームアウトした時にノードコメントのようにコメントを表示できます。
[Color Bubble]を有効にすると、コメントの色を[Comment Color]の色で表示できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-48-37.png)

[Move Mode]はコメントボックスを動かした時の設定です。
デフォルトで設定されている[Group Movement]はコメントボックスを動かすと、コメントボックスで囲まれているノードを一緒に動かせます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-48-55.png)

[Move Mode]を[Comment]に変更すると、コメントボックスだけを移動できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-49-12.png)

コメントを残すことは大事ですが、処理を変更した時にコメントを変更し忘れてしまうことがよくあります。処理とコメントが違うと混乱してしまうので、処理を修正したらコメントも必ず修正しましょう。

### すべて保存する

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-10-14-22.png)

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/Editor/UIBreakdowns/ClassBPUI/

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Comments/

https://docs.unrealengine.com/4.26/ja/ProgrammingAndScripting/Blueprints/UserGuide/Types/
