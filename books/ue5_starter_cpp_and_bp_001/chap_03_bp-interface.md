---
title: "【BP】インターフェース"
free: false
---

## インタフェース

### インタフェースについて

Interface クラスは関連性のない一連のクラスが共通の関数を確実に実装するために役立ちます。
UnrealEngineはAActorから派生したりするので、共通の機能を持つ必要が発生した時にインタフェースを使用することが勧められています。

### インタフェースを作成する

BlueprintInterfaceを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-21-19.png)

名前を「BPI_Interface」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-26-54.png)

BlueprintInterfaceを設定するEditorが開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-30-31.png)

名前を「PrintHello」に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-31-32.png)

[Add] > [Function]からFunctionを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-32-37.png)

名前を「Add」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-33-19.png)

InputとOutputを設定します。

**Input**

| name | Variable Type |
| ---- | ------------- |
| A    | Integer       |
| B    | Integer       |

**Output**

| name        | Variable Type |
| ----------- | ------------- |
| ReturnValue | Integer       |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-36-11.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-46-27.png)

### インタフェースを実装するクラスを作成する

BlueprintInterfaceを設定するBlueprintを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-48-46.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-51-43.png)

名前を「BP_InterfaceTest」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-52-46.png)

「Class Settings」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-55-13.png)

Interfaceに「BPI_Interface」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-56-59.png)

Interfaceで追加した関数が「Interface」カテゴリに追加されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-58-57.png)

Outputを設定していない関数はEventとして実装できます。
関数を右クリック > [Implement event]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-00-31.png)

Implement eventを選択するとEvent Graphに関数名のイベントが追加されます。
追加されたEventに処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-02-15.png)

Outputを設定した関数は関数として処理を実装できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-03-34.png)

BeginPlayに動作確認する為の処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-10-52.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-12-01.png)

[BP_InterfaceTest]をViewportにDrag&Dropします。
VieportにCPPInterfaceTestがあれば削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-16-21.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

インターフェースで実装したメンバ関数を呼び出せました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-23-14-52.png)

### メンバ関数をオーバーライドする

### 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/UsingInterfaces/
