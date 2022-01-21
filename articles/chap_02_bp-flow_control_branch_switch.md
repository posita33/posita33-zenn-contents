---
title: "2.7.BP Flow Control(Branch,Switch)"
emoji: "😊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---

## 【Blueprint版】Flow Control(Branch,Switch)

「もし、あの時○○をしていたら。。。」

「選択肢1～4のどれかを選択しなさい。」

常に選択を迫られています。
プログラミンでは分岐する処理を実装することができます。
今回は、Floｗ Control(制御文)について学習します。

### 今回出来ること
変数の値に応じて四則演算の出力処理を切り替えて出力します。
2つのFlow Controlノードを使用します。

|ノード名|出来ること|
|----|----|
|Branch|2択（TrueかFalse）の処理を分岐する|
|Switch|複数選択(値に応じて)の処理を分岐する|

### 学習用の新規レベル「Chapter_2_8_FlowControl_01」を作成する

学習用の新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch_switch/2022-01-21-05-31-55.png)

[Default]を選択します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch_switch/2022-01-21-05-32-35.png)


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch_switch/2022-01-21-05-35-40.png)

### Flow Controlに使用する変数を作成する

