---
title: "【BP】Enumeration(列挙型)"
emoji: "✨"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---

## 【Blueprint】Enumeration（列挙型）

### 今回できること
変数[CalcType]のVariableTypeをEnumerationに変更することで、[Swith]ノードの分岐をより読みやすくします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-35-50.png)

Enumeration（列挙型）をVariableTypeに設定することで、DefaultValueがリストから選択できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-37-33.png)

### 学習用の新規レベル「Chapter_2_Enumeration」を作成する

学習用の新規レベルを作成します。
[File]メニューから[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-08-49-02.png)

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-08-49-18.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-32-19.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Enumeration」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-08-52-19.png)


### Enumeration（列挙型）を作成する

Enumeration（列挙型）を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-04-13.png)
*Contents Browserの空きスペースを右クリック > Blueprints > Enumeration（列挙型）*

アセット名を「ECalcType」に設定します。
「EcalcType」をダブルクリックで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-05-38.png)


[New]ボタンをクリックすることで列挙定数を追加できます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-15-13.png)

列挙型を設定するEditorの入力項目について一覧にまとめました。

| Property         | required | About                |
| ---------------- | -------- | -------------------- |
| Display Name     | 〇       | 列挙定数の表示名     |
| Description      | -        | 列挙定数の説明       |
| Enum Description | -        | 作成した列挙型の説明 |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-22-33.png)

[New]ボタンで列挙定数を追加し、各行表の値を設定します。

| Display Name | Description      |
| ------------ | ---------------- |
| Add          | Addition         |
| Subtract     | Subtraction      |
| Multiply     | Multiplicatation |
| Divide       | Division         |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-24-23.png)

### Blueprintを複製する

「BP_FlowControl_Switch」をDuplicate（複製）して、「BP_FlowControl_SwitchEnum」を作成します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-01-54.png)


### 変数[CalcType]のVariableTypeを[Integer]から[ECalcType]に変更する

「BP_FlowControl_SwitchEnum」をダブルクリックして開きます。
変数「CalcType」のVariableTypeを「ECalcType」に変更します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-48-38.png)

EventGrapth内で変数を使用ていると、VariableTypeを変更してもいいかを確認するダイアログが表示されます。
[Change Variable Type]ボタンをクリックして、VariableTypeを変更します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-53-09.png)

変数[CalcType]のGetがエラー（赤）で表示されます。
赤くなっているピンを[Alt + Click]で接続を解除します。
同時に変更した箇所の一覧が表示されます。行をクリックすることで該当箇所へ移動できます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-55-09.png)

[Compile]ボタンをクリックして、変数[VariableType]のDefaultValueを確認します。
DefaultValueの値がリスト化され、EnumerationのDisplayNameに設定した文字列が選択できます。
VariableTypeがIntegerの時は数値で入力していたので、[1]というのは何の値なのか分かりませんでした。
Enumeration（列挙型）にすることで、何の値を設定するのか明確になります。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-11-31.png)

### ECalcTypeのSwitchノードに処理を置き換える

変数[CalcType]のGetノードからDrag&Dropし、[Switch on ECalcType]を選択します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-09-59-42.png)

[Switch]ノードのOutput側実行ピンにEnumerationのDisplayNameで設定した文字列が表示されます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-01-22.png)

Integerの[Switch]ノードより[Switch]ノードからどの処理に接続してよいか分かりやすくなります。
Enumeration（列挙型）はDisplayNameに設定した列挙定数しか設定できないので、「Default」実行ピンのようなあいまいな表現がなくなります。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-03-46.png)

[Compile]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-20-57.png)

LevelEditorに戻り、「BP_FlowControl_SwitchEnum」をViewportにDrag&Dropします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-19-33.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-21-20.png)

変数[CalcType]の値が[Subtract]なので、引き算の出力結果が表示されます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-21-59.png)

### すべて保存
Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-enumeration/2022-01-24-10-31-44.png)


## 参照URL

オンラインラーニング「**ブループリントで列挙型を使用する**」

https://www.unrealengine.com/ja/onlinelearning-courses/using-enumerations-in-blueprints

