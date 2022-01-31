---
title: "【BP】Flow Control（Loop）"
free: false
---

## 【Blueprint】Flow Control（Loop）

### 今回できること

Flow Control（Loop）は繰り返し処理を行うことができます。
10000回の計算をランダムに計算できるのがコンピューターの強みです。
ブループリントには3種類のLoopノードが用意されています。

- For Loop
- For Each Loop
- While Loop

[For Loop]と[For Earch Loop]にはBreak付きのノードが用意されています。


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-40-34.png)

3つのLoopで同じ結果になる処理を紹介します。

- For Loop
- For Each Loop
- While Loop

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-40-54.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-41-03.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-41-14.png)

### 学習用の新規レベル「Chapter_2_FlowControl_Loop」を作成する

学習用の新規レベルを作成します。
[File]メニューから[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-14-41.png)

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-14-52.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-15-15.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_FlowControl_Loop」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-18-08.png)

### Blueprintを複製する

「BP_Array」を複製（Ctrl + W）して、「BP_FlowControl_Loop」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-23-03.png)

### For LoopノードでPrintStringを繰り返し呼び出す

For Loopノードを使用して[PrintString]ノードを繰り返し呼び出します。

メニューから[For Loop]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-27-09.png)

[For Loop]ノードの[Last Index]ピンの値を[4]に設定します。
Custom Event[PrintHello]が呼ばれたら、[For Loop]ノードを呼び出します。
[For Loop]ノードの[Loop Body]と[printString]ノードを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-40-45.png)

[PrintString]ノードを追加し、図のように[For Loop]ノードの[Completed]と[PrintString]ノードを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-11-45-17.png)

[For Loop]ノードの[Index]の値を確認したいので、[PrintString]ノードの[In String]に接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-26-10.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-20-39.png)

Level Editorに戻り、「BP_Array」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-21-56.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-31-22.png)

[H]キーをPressすると[PrintString]ノードが繰り返し呼び出されました。
[For Loop]ノードの[First Index]で[0]、[Last Index]が[4]と設定されているので、0～4の5回繰り返されます。
[For Loop]ノードの[Index]の値は[LoopBody]が呼び出された後に値が[+1]されます。
[Last Index]の[4]が呼び出された後に、[For Loop]ノードの[Completed]が呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-30-36.png)

### For Loopノードで配列をすべて出力する

[For Loop]ノードで配列をすべて出力するように編集します。

[For Loop]ノードの[Last Index]に配列のLastIndexを設定します。
配列のLastIndexの求め方は「配列のLength - 1」でした。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-34-27.png)

[For Loop]ノードの[Index]を使用して、配列[Messages]の[Get]ノードから値を取得します。
配列[Messages]の[Get]ノードを[PrintString]ノードの[In String]に接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-37-58.png)

[For Loop]ノードを使用した配列をすべて出力する処理です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-45-25.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-20-39.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-31-22.png)

[H]キーをPressすると配列[Messages]の値を最初から最後まで出力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-50-46.png)

### For Loop with BreakノードでLoopを途中で抜ける

[For Loop]ノードには、Input側に[Break]実行ピンを持つ[For Loop with Break]ノードが用意されています。
[Break]実行ピンの動きを確認しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-16-46-49.png)

メニューから[For Loop with Break]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-53-40.png)

[For Loop]ノードの接続を、[For Loop with Break]を使用するように接続し直します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-02-42.png)

[For Loop with Break]ノードの[Break]実行ピンを呼び出すために分岐を作成します。
文字列の中に[Bonjour]が含まれていた時に、[For Loop with Break]ノードの[Break]実行ピンを呼び出すように編集します。

[Get]ノードからDrag&Dropし、Stringカテゴリーの[Contains]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-16-55-33.png)

[Contains]ノードは[Search In]に設定した文字列内で[Substring]の文字列が含まれているか確認するノードです。
[Substring]に[Bonjour]を設定します。
[Break]を呼び出す分岐を作るので、[Contains]ノードの[ReturnValue]から[Branch]ノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-13-32.png)

[Branch]ノードの接続を以下のように接続します。

- [Branch]ノードの[Condision]が[True]の時に、[For Loop with Break]ノードの[Break]実行ピンを呼び出す。
- [Branch]ノードの[Condision]が[False]の時に、[PrintString]ノードを呼び出す。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-18-28.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-20-39.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-31-22.png)

[H]キーをPressすると配列[Messages]の値に[Bonjour]が含まれている時にBreakが呼ばれるので、配列[Messages]のIndex[2]までが[PrintString]ノードで出力されます。

[For Loop with Break]ノードは[Break]実行ピンが呼ばれるとループを終了し、[Complited]実行ピンが呼ばれます。
[Break]実行ピンが呼ばれなければ、[For Loop]ノードと同じ動きをします。
[For Loop with Break]ノードはループを抜ける条件がある時に使用します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-35-13.png)

### Foreach Loop with Breakノードで配列をすべて出力する

配列をループさせるのであれば、[For Loop]ノードより、[For Earch Loop]ノードを使用した方がスマートに処理を書くことができます。
[For Earch Loop]ノードにも[Break]実行ピンを持った[For Earch Loop with Break]ノードがあります。
[For Loop with Break]ノードを使用した処理を[For Earch Loop with Break]を使用した処理に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-17-14-08.png)

メニューから[For Each Loop with Break]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-41-37.png)

[For Each Loop with Break]を使用した処理に接続し直します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-49-00.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-20-39.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-31-22.png)

[H]キーをPressすると配列[Messages]の値に[Bonjour]が含まれている時にBreakが呼ばれるので、配列[Messages]のIndex[2]までが[PrintString]ノードで出力されます。
配列を順番に繰り返しするのであれば、[For Loop]ノードより[For Each Loop]の方がスマートに処理を実装できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-14-57-36.png)

### While loopノード

最後に[While Loop]について説明します。
[For Loop]や[For Each Loop]より使用頻度が少ないのでアッサリと説明します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-17-26-38.png)

[While Loop]ノードはIndexNoがいくつか教えてくれないので、IndexNoを持つ変数を追加します。

| VariableName | VariableType | Category     | DefaultValue |
| ------------ | ------------ | ------------ | ------------ |
| HelloIndex   | Integer      | Flow Control | 0            |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-16-45.png)

メニューから[While Loop]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-19-59.png)

[While Loop]ノードを使用した時の配列の値を出力する処理です。
[For Loop with Break]ノードや[For Each Loop with Break]ノードを使用した時と同じ動きになる図です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-22-14.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-20-39.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-13-31-22.png)

[H]キーをPressすると配列[Messages]の値に[Bonjour]が含まれている時に、[While Loop]ノードの[Condision]が[False]になるので、[While Loop]ノードの[Conpleted]が呼ばれます。
[While Loop]ノードは[Condition]の値が[True]の時に[Loop Body]を呼び出し、[Condition]の値が[False]の時に[Completed]を呼び出します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-27-24.png)

### すべて保存

Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-30-10.png)

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/
