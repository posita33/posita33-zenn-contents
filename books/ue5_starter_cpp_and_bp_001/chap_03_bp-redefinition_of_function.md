---
title: "【BP】メンバ関数の再定義"
free: false
---

## メンバ関数の再定義

### 基底クラスのメンバ関数を再定義する

基底クラスのメンバ関数は、派生クラスで定義し直せます。
メンバ変数を設定するSetPointを派生クラスで再定義します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-23-54-22.png)

### 基底クラス「BP_ParentRedefinition」を作成する

基底クラス「BP_ParentRedefinition」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-08-46-16.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-08-47-37.png)

Class名を「BP_ParentRedefinition」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-14-59.png)

| Variable Name | Variable Type |
| ------------- | ------------- |
| Point         | Integer       |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-01-34.png)

Functionに「SetPoint」を追加します。
Inputを設定します。

| Variable Name | Variable Type |
| ------------- | ------------- |
| myPoint       | Integer       |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-07-50.png)

SetPointの処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-10-30.png)

Functionに「GetPoint」を追加します。
Inputを設定します。

| Variable Name | Variable Type |
| ------------- | ------------- |
| ReturnValue   | Integer       |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-17-48.png)

GetPointの処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-19-34.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-23-31.png)

### 派生クラス「BP_ChildRedefinition」を作成する

派生クラス「BP_ChildRedefinition」を作成します。

基底クラス「BP_ParentRedefinition」右クリック > [Create Child Blueprint Class]を選択

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-25-25.png)

Class名を「BP_ChildRedefinition」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-28-13.png)

FunctionのOverrideをクリック > [SetPoint]を選択します

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-45-17.png)

SetPointの処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-46-22.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-48-55.png)

### 基底クラスと派生クラスを呼び出すテストクラスを作成する

基底クラス「BP_ParentRedefinition」と派生クラス「BP_ChildRedefinition」を生成して、メンバ関数の動作確認するためのテストクラス「BP_RedefinitionTest」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-09-53-10.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-08-47-37.png)

Class名を「BP_RedefinitionTest」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-redefinition_of_function/2022-09-18-10-07-07.png)



@[blueprintue](https://blueprintue.com/blueprint/6ytlakkp/)















