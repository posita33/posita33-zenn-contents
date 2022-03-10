---
title: "クラスとオブジェクト"
free: false
---

## クラスの概念

構造体は複数の型の変数をまとめたものでしたが、クラスは変数と関数をひとまとめできます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_class_and_object/2022-03-08-07-18-51.png)

## クラスのメンバ

クラスに含まれる要素は「**メンバ**」と呼ばれます。
変数(Variable)なら「**メンバ変数**」、関数(Function)なら「**メンバ関数**」と呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_class_and_object/2022-03-11-05-18-01.png)

RPGのキャラクターで考えてみると少し分かりやすいです。
名前やHPようなキャラクターのステータスは「メンバ変数」です。
「たたかう」「まほう」のようなアクションは「メンバ関数」です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_class_and_object/2022-03-11-06-12-19.png)

## クラスのオブジェクト化

UnrealEngineのActorクラスはViewportに配置して初めて実体化します。
クラスを実体化したものを「**オブジェクト**」と呼びます。
クラスは「**オブジェクトの設計図**」になります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_class_and_object/2022-03-11-06-24-49.png)

正確にはプレイした時に実体化されてオブジェクトになります。
クラスという設計図を元にキャラクターがオブジェクトになって動きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_class_and_object/2022-03-11-06-05-54.png)

## 関連リンク

変数と関数の定義については基本文法の項目を参照してください。

【変数】

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_bp-variable

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_cpp-variable

【関数】

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_bp-function

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_cpp-function

## Column

:::message
**Column：C++の構造体はクラスのように関数を定義できる**
:::

開始時に構造体とクラスの違いを関数を持っているかの違いで説明しましたが、エンジンソースを読んでいると関数を定義している構造体があります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_class_and_object/2022-03-11-06-37-14.png)

C++のクラスはC言語の構造体の拡張です。
クラスと構造体の違いは、アクセシビリティのデフォルトが違います。
構造体はデフォルトが「public」、クラスはデフォルトが「private」になります。

https://www.ibm.com/docs/ja/xl-c-and-cpp-aix/12.1.0?topic=only-classes-structures