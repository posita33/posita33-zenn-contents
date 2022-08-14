---
title: "【BP】アクセス指定子"
free: false
---

## アクセス指定子

### アクセス指定子について

アクセス指定子には次の3種類があります。

| アクセス指定子 | 自クラス | 継承したクラス | 外部クラス |
| -------------- | -------- | -------------- | ---------- |
| public         | 〇       | 〇             | 〇         |
| protected      | 〇       | 〇             | ×          |
| private        | 〇       | ×              | ×          |

BPで3つのアクセス指定子の使用方法や参照できる範囲を把握してみます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-05-53-41.png)

### 基底クラス（親クラス）を作成する

基底クラス(親クラス)を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-05-56-32.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-05-57-36.png)

名前を「BP_AccessParent」に設定して開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-05-58-42.png)

### 変数にアクセス指定子を設定する

変数を追加します。

| name            | Variable Type |
| --------------- | ------------- |
| VarPublicNum    | Integer       |
| VarProtectedNum | Integer       |
| VarPrivateNum   | Integer       |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-06-16-04.png)

Blueprintのアクセス指定子をPrivateにするにはPrivateプロパティのチェックを有効にします。
今回は[VarPrivateNum]のPrivateプロパティのチェックを有効にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-06-19-59.png)

アクセス指定子を「Public」と「Protected」に変更したいのですが、BlueprintにはPrivate以外の設定がありません。

公式ドキュメントによると[Instance Editable]を有効にすることがPublic変数となるようです。

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Variables/#public%E5%A4%89%E6%95%B0

今回は[VarPublicNum]の[Instance Editable]を有効にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-06-23-17.png)

「BP_AccessParent」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-06-27-04.png)

[Instance Editable]を有効にした変数はViewport配置後にDetailsパネルで値を変更できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-06-29-39.png)

変数のDefault値を以下の表になるように設定します。

| name            | Private | Instance Editable | Default Value |
| --------------- | ------- | ----------------- | ------------- |
| VarPublicNum    | ×       | 〇                | 11            |
| VarProtectedNum | ×       | ×                 | 22            |
| VarPrivateNum   | 〇      | ×                 | 33            |

:::message
Blueprintの変数にはPrivateの設定はありますが、
アクセス指定子を「Public」「Protected」に設定する設定がありません。
公式ドキュメントでは「Instance Editable」を有効にするのがPublic変数として記載されています。
何も設定しないデフォルトの設定がProtectedになるかというと、外部から参照できるのでPublic扱いになります。
:::

### 関数にアクセス指定子を指定する

関数を追加します。

| name              |
| ----------------- |
| CallPublicFunc    |
| CallProtectedFunc |
| CallPrivateFunc   |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-26-04.png)

関数は3種類のアクセス指定子を設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-27-29.png)

以下のようにアクセス指定子を設定します。

| name              | Access Specifier |
| ----------------- | ---------------- |
| CallPublicFunc    | Public           |
| CallProtectedFunc | Protected        |
| CallPrivateFunc   | Private          |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-32-58.png)

PrintStringでActor表示名、メンバ関数、データメンバを出力する処理を実装します。

**CallPublicFunc**

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-40-25.png)

**CallProtectedFunc**

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-41-12.png)

**CallPrivateFunc**

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-41-49.png)

BeginPlayで作成したメンバ関数を呼び出します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-45-03.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-10-46-08.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

自クラスのメンバ関数、データメンバにはすべて参照できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-14-56-11.png)

### 派生クラス（子クラス）を作成する

派生クラスを作成します。
基底クラスになるBlueprintを右クリック > [Create Child Blueprint Class]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-02-35.png)

名前を「BP_AccessChild」に設定して開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-15-04-14-49.png)

処理は変更せず、BeginPlayで[Parent：BeginPlay]を読んでいることを確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-03-38.png)

基底クラスの「BP_AccessParent」を削除して、「BP_AccessChild」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-05-35.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

Prantノードからでは基底クラスのメンバ関数、データメンバを参照できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-15-55.png)

次に基底クラスのメンバ関数、データメンバを参照できるか確認します。

データメンバはPrivateにチェックを入れていない変数のみ参照できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-32-11.png)

メンバ関数はアクセス指定子に「Public」と「Protected」を設定したメンバ関数が呼び出せます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-18-57.png)

基底メンバのメンバ変数を変更した後に、基底クラスのメンバ関数を呼び出します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-33-16.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-25-15.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

派生クラスからはPrivateに設定していないメンバ関数、データメンバに参照できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-15-37-24.png)

### 外部クラスから基底クラスを参照する

外部クラスから基底クラスのメンバ関数、データメンバを参照できるか確認します。
基底クラスを参照する外部クラスを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-11-34.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-13-50.png)

名前を「BP_AccessOther」に設定して開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-15-11.png)

「Get Actor of Class」ノードで「BP_AccessParent」を取得し、「BP_AccessParent」のデータメンバのSetを呼び出します。
検索した一覧からはPrivateにチェックを入れていないデータメンバの「VarPublicNum」、「VarProtectedNum」のSetが一覧に表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-21-30.png)

「BP_AccessParent」のメンバ関数を呼び出します。
メンバ関数は「Public」に指定している「CallPublicFunc」のみ呼び出せます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-28-07.png)

以下の図のように処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-29-33.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-30-17.png)

PrintStringを確認しやすくするために、「BP_AccessParent」でPrintStringを呼び出さないように修正します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-34-47.png)

「BP_AccessChild」を削除し、Viewportに「BP_AccessParent」と「BP_AccessOther」をDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-31-56.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

外部クラスからはアクセス指定子にPublicを指定したメンバ関数か、Privateにチェックをしていないデータメンバが参照できます。


![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-18-36-53.png)

### Blueprintのアクセス指定子

アクセス指定子には次の3種類があります。

| アクセス指定子 | 自クラス | 継承したクラス | 外部クラス |
| -------------- | -------- | -------------- | ---------- |
| public         | 〇       | 〇             | 〇         |
| protected      | 〇       | 〇             | ×          |
| private        | 〇       | ×              | ×          |

BPでも3つのアクセス指定子の参照できる範囲はC++と同じです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp_access_specifier/2022-08-14-05-53-41.png)

しかし、データメンバではPrivateの設定しかありません。
Instance Editableの設定を有効にすることで「Public変数」と呼びますが、デフォルトの設定のままでも外部クラスから参照できるのでPublicと同じ扱いになります。

| name            | Private | Instance Editable |
| --------------- | ------- | ----------------- |
| VarPublicNum    | ×       | 〇                |
| VarProtectedNum | ×       | ×                 |
| VarPrivateNum   | 〇      | ×                 |

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Variables/

https://docs.unrealengine.com/4.26/ja/ProgrammingAndScripting/Blueprints/UserGuide/Functions/