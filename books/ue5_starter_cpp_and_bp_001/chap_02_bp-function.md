---
title: "【BP】Function（関数）"
free: false
---

## 【Blueprint】Function（関数）

### 今回できること

[Add]ノードを再現するFunctionを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-11-57.png)

計算結果の出力処理をFunction化します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-12-25-37.png)


### 学習用の新規レベル「Chapter_2_Function」を作成する

学習用の新規レベルを作成します。
[File]メニューから[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-08-52-51.png)

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-08-52-59.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-32-19.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Function」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-08-55-15.png)


### Blueprintを複製する

「BP_FlowControl_SwitchEnum」を複製（Ctrl + W）して、「BP_Function」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-02-46.png)


### Function[Sum]を作成する

Blueprintの[Add]ノードを再現したFunction[Sum]を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-20-21.png)

Functionに[Sum]を追加します。
[My Blueprint]パネルのFunctionsカテゴリ右側の[+]をクリックします。
Functionが新しく作成されるので、名前を[Sum]に設定します。
GraphにはFunction名のノードが作成されます。
Functionの開始地点となるノードです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-22-38.png)

InputとOutputを追加します。

| Input/Output | VariableName | VariableType |
| ------------ | ------------ | ------------ |
| Input        | A            | Integer      |
| Input        | B            | Integer      |
| Output       | ReturnValue  | Integer      |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-33-04.png)

Addノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-36-54.png)

InputのA,Bを[Add]ノードで計算するように接続します。
[Add]ノードのOutputを[Return Node]の[ReturnValue]に接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-38-38.png)

Functionに設定したInput,Outputを反映するために、[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-54-55.png)

Function[Sum]をEvent Grapthに追加します。
追加方法は2種類あります。

- [My Blueprint]からFunction[Sum]をDrag&Dropする。
- メニューで[Sum]を検索して選択する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-43-32.png)

Function[Sum]を処理するように、実行ピンを接続しなおします。
Function[Sum]のInput[A][B]に変数[CalcValueA],[CalcValueB]を接続します。
Function[Sum]のOutput[ReturnValue]を[IntegerからString変換]ノードに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-48-25.png)

Function[Sum]の実行ピンを通過するように、変数[CalcType]のDefaultValueを[Add]に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-function/2022-02-13-17-00-39.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-54-55.png)

LevelEditorに戻り、「BP_Function」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-function/2022-02-13-17-02-07.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-57-35.png)

Function[Sum]で計算した結果が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-07-14.png)

Functionを使用した時の処理の流れは図のようになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-11-57.png)

### Function内でのみ使用できるLocal Variable（ローカル変数）を作成する

Functionでのみ使用できる変数「Local Variable（ローカル変数）」を使用します。

Local Variables[LocalResult]を作成します。
Function[Sum]を開きます。
Function[Sum]を開くと、[My Blueprint]パネルに[Local Variables]カテゴリが表示されます。
[Local Variables]カテゴリの[+]ボタンをクリックします。
追加されたLocal Variableの名前を「LocalResult」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-36-38.png)

Local Variable[LocalResult]のSetノードを追加します。
Input[A],[B]の[Add]ノードの結果を[LocalResult]に設定します。
Function[Sum]の[ReturnValue]に[LocalResult]の値を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-39-52.png)

[Event Graph]に戻ると[Local Variables]カテゴリは表示されません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-42-09.png)

[Local Variables]カテゴリはFunction内でのみ使用できる変数を宣言できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-44-38.png)

VariablesとLocal Variablesの違いについて表にまとめました。

| 変数のタイプ    | 説明                                                      |
| --------------- | --------------------------------------------------------- |
| Variables       | Variablesに宣言した変数はクラス内・クラス外から参照できる |
| Local Variables | 宣言したFunction内でのみ参照できる                        |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-48-11.png)


### Function[Sum]のpure化（純粋化）

Blueprintの[Add]ノードのようにFunction[Sum]を[実行]ピンがないノードに変更します。

Function[Sum]のノードを選択し、[Detail]パネルから[Pure]のチェックボックスをチェックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-51-24.png)

[Pure]のチェックボックスにチェックが入ると、Function[Sum]の実行ピンがなくなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-54-49.png)

公式ドキュメントの純粋関数（Pure Function）の解説です。

>関数は 純粋関数 または 非純粋関数 のどちらかになります。両者の大きな違いは、純粋関数がステートやクラスのメンバーを一切変更しないのに対し、 非純粋関数はステートを自由に変更します。純粋関数は通常、データ値を出力するだけの getter 関数や演算子に使用されます。 関数または演算子は、データ値を単に出力します。

> 純粋関数はデータピンへ接続され、依存するデータが要求されるとコンパイラにより自動的に実行されます。このため、 純粋関数は接続先のノードにつき 1 回ずつ呼び出されます。純粋関数は以下のいずれかのメソッドを使って指定されます。
>・コードで定義された関数に対する関数宣言のキーワードに BlueprintPure を指定します。
>・ブループリント エディタ で追加された関数の [Pure] のチェックボックスにチェックを入れます。

https://docs.unrealengine.com/4.26/ja/ProgrammingAndScripting/Blueprints/UserGuide/Functions/

### 計算結果の文字列を取得する関数を作成する

もう少し複雑な関数を作成します。
計算結果の出力処理を関数化しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-10-59-05.png)

まず、共通で使用しているInputの洗い出しを行います。

以下の4つの変数を共通的に使用しています。

- CalcType
- CalcVarA
- CalcVarB
- Duration

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-11-02-46.png)

共通で使用している変数を1か所だけ接続した状態にして、端にまとめます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-11-14-01.png)

Inputに繋げていたノード以外を範囲選択します。
範囲選択したどれかのノードを右クリックし、[Collapse Function]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-11-18-24.png)

選択したノードたちが1つの[New Function 0]というノードに変換されます。
[New Function 0]をダブルクリックして中身を確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-11-19-54.png)

範囲選択したノードが[New Function 0]の中で再現されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-11-21-41.png)

Input[A],[B],[Duration]を接続されていない、「引き算」,「掛け算」と「割り算」に接続し直します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-11-25-28.png)

Function Nameを[PrintCalcResult]に変更します。
Inputの順番を入れ替えたり、適切な名称に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-12-15-33.png)

計算結果を出力する処理が1つの関数にまとめられました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-12-16-13.png)

EventGraphに戻って見ると、「HelloWorldを出力する」「計算結果を出力する」の2つの処理がBranchで切り分けられているのが分かりやすくなりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-13-37-56.png)

Function化したことで、処理がまとめられて分かりやすくなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-12-25-37.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-54-55.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-09-57-35.png)

先ほどと同じ足し算の計算結果が表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-Function/2022-01-25-12-28-09.png)

### すべて保存

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-function/2022-02-13-17-09-37.png)

## 参照URL

https://docs.unrealengine.com/4.26/ja/ProgrammingAndScripting/Blueprints/UserGuide/Functions/
