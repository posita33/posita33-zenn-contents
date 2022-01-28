---
title: "【BP】Flow Control(Switch)"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---

## 【Blueprint】Flow Control（Switch）

### 今回できること
[Branch]ノードを複数使用して分岐した処理を[Switch]ノードで分岐させます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-17-04-24.png)

### 学習用の新規レベル「Chapter_2_FlowControl_Switch」を作成する
学習用の新規レベルを作成します。
[File]メニューから[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-14-53.png)

[Default]を選択します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-15-04.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-32-19.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_FlowControl_Switch」を入力し、[Save]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-17-30.png)

### Blueprintを複製する
「BP_FlowControl_Branch」をDuplicate（複製）して、「BP_FlowControl_Switch」を作成します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-20-45.png)


### Switchノードを使用して数値で分岐する

[Branch]ノードを複数使用して、変数[CalcType]の値に応じて計算結果の出力処理を切り替えました。
[Switch]ノードを使用して、処理を見やすく変更しましょう。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-23-50.png)

メニューから[Switch on int]を選択します。
[Switch]ノードを追加する時は、追加したいVariableTypeのSwitchノードを[Switch （ValiableType）]で検索すると、メニューから見つけることができます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-26-37.png)

[Switch]ノードのOutputピンの数を[Add pin]の[+]をクリックして追加します。
Outputピンは以下のように計算結果の出力を切り替えます。
- 0:足し算
- 1:引き算
- 2:掛け算
- Default（該当しない値）:割り算

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-33-01.png)

[Switch]ノードから計算結果を出力する処理を切り替えるように実行ピンを接続し直します。
1つの変数の値に応じて処理を切り替えるときに[Switch]ノードを使用すると処理が見やすくなります。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-37-53.png)

[Compile]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-54-14.png)

LevelEditorに戻り、「BP_FlowControl_Switch」をViewportにDrag&Dropします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-57-11.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-54-23.png)

変数[CalcType]の値が[1]なので、引き算の出力結果が表示されます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-58-06.png)

[Switch]ノードを使用することで処理の流れが見やすくなりました。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-59-55.png)

### Switchノードの設定について

[Switch]ノードを選択すると、[Detail]パネルにプロパティが表示されます。
プロパティの設定を変更することで[Switch]ノードの使い方を変更できます。

| Property        | About                                 |
| --------------- | ------------------------------------- |
| Start Index     | 実行ピンの一番上のIndex番号を設定する |
| Has Default Pin | Defaultピンの表示（true）/非表示（false） |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-16-49-37.png)


### すべて保存

Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_switch/2022-01-23-17-03-08.png)