---
title: "【BP】Structure（構造体）"
free: false
---

## 【Blueprint】Structure（構造体）

### 今回できること

### 学習用の新規レベル「Chapter_2_Structure」を作成する

学習用の新規レベルを作成します。
[File]メニューから[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-29-05.png)

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-29-17.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-29-29.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Structure」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-32-13.png)

### Blueprintを複製する

「BP_FlowControl_Loop」を複製（Ctrl + W）して、「BP_Structure」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-35-51.png)

### 構造体「FBPCalcStructure」を作成する

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-40-37.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-51-46.png)

変数を追加する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-53-30.png)


| VariableName | VariableType | DefaultValue |
|--------------|--------------|--------------|
| Type         | EBPCalcType  | Add          |
| NumA         | Integer      | 7            |
| NumB         | Integer      | 3            |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-06-43-32.png)

### Function「PrintCalcResult」を複製してFunction「PrintCalcResultInStructure」を作成する




### Function「PrintCalcResultInStructure」に処理を置き換える

### すべて保存

Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Variables/Structs/
