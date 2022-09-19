---
title: "【BP】仮想関数とオーバーライド"
free: false
---

## 仮想関数とオーバーライド

### 基底クラスのメンバ関数を再定義する

Blueprintではメンバ関数を作成するさいにVirtualを付けることができません。
では、Blueprintのメンバ関数を再定義した時には仮想関数で定義されているのでしょうか。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-18-00-49.png)

### Blueprintの再定義したクラスが仮想関数か確認するテストクラスを作成する

メンバ関数の再定義で作成したBlueprintを使用して、Blueprintのメンバ関数が仮想関数で定義されているか確認します。

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_03_bp-redefinition_of_function

動作確認するためのBlueprintを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-41-38.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-43-18.png)

Class名を「BP_VirtualTest」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-44-47.png)

変数に基底クラスの変数を追加します。

| Variable Name | Variable Type         |
| ------------- | --------------------- |
| Parent        | BP_ParentRedefinition |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-51-31.png)

派生クラス「BP_ChildRedefinition」を生成して、基底クラスに一度格納した後にSetPointを呼び出すことで仮想関数かどうかを動作確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-50-13.png)

@[blueprintue](https://blueprintue.com/render/g1yj2ycs/)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-53-13.png)

「BP_VirtualTest」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-56-11.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

派生クラスのメンバ関数の結果が出力されたので、Blueprintのメンバ関数は仮想関数として定義されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-17-56-31.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-virtual_function_override/2022-09-19-18-05-18.png)
