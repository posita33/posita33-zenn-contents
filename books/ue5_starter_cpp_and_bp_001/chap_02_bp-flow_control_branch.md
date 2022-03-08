---
title: "【BP】Flow Control（Branch）"
free: false
---

## 【Blueprint】Flow Control（Branch）

「もし、あの時○○をしていたら。。。」

「選択肢1～4のどれかを選択しなさい。」

常に選択を迫られています。
プログラミンでは分岐する処理を実装できます。
今回は、Flow Control（制御文）について学習します。

### 今回できること

変数の値に応じて、PrintStringを切り替えて出力します。

[Branch]ノードは[Condition]ピンに接続したノードの値に応じて、実行される実行ピンが切り替わります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-37-11.png)

比較演算子を使用することで、数値を比較して分岐できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-16-43-53.png)

論理演算子を使用することで、複雑な条件で分岐できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-18-11-10.png)

[Branch]ノードを組み合わせることで、複数の選択肢の分岐ができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-18-33-32.png)

### 学習用の新規レベル「Chapter_2_FlowControl_Branch」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-03-09-06-14-25.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_FlowControl_Branch」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-02-56.png)

### Blueprintを複製する

「BP_Calculation」を複製（Ctrl + D）して、「BP_FlowControl_Branch」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-05-01.png)

### Flow Controlに使用する変数を宣言する
今回使用する変数を宣言します。

| VariableName | VariableType | Category     | DefaultValue |
| ------------ | ------------ | ------------ | ------------ |
| IsPrintHello | Boolean      | Flow Control | true         |
| CalcType     | Integer      | Flow Control | 0            |
| NumA         | Integer      | Flow Control | 1            |
| NumB         | Integer      | Flow Control | 2            |
| NumC         | Integer      | Flow Control | 15           |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-12-54.png)

### Branchノードで処理を切り替える

[Branch]ノードを使用して、「Hello Wordl!」を出力するPrintStringと、計算結果をPrintStringする処理を切り替えます。

Sequenceノードの[Then 0]実行ピンと「Hello World!」を出力する[PrintString]ノードの実行ピンの接続を解除します。
[Branch]ノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-16-20.png)

変数[IsPrintHello]のGetノードを追加し、[Branch]ノードの[Condition]ピンに接続します。
[Branch]ノードを図のように実行されるよう実行ピンを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-21-52.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-24-04.png)

LevelEditorに移動し、「BP_FlowControl_Branch」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-13-12.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

「Hello World!」を出力する[PrintString]ノードの処理のみが実行されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-14-27.png)

Playボタンを押した時にBlurprintEditorを表示しておくと、Blueprintがどのような動きをしているか確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-16-11.png)

[Branch]ノードは[Condition]ピンに接続したノードの値に応じて、実行される実行ピンが切り替わります。
今回は変数[IsPrintHello]に[True]の値が設定されていたので、[Branch]ノードは[True]の実行ピンに処理を切り替えて、[Hello World!]を出力する[PrintString]ノードを実行しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-37-11.png)

```mermaid
graph TB
    A[BeginPlay] --> B{IsPrintHello}
    B -->|True| D[PrintString Hello World!]
    B -->|False| E[PrintString Calculation]
```

### 比較演算子ノードで処理を切り替える

2つの変数[NumA]と[NumB]の値を比較して分岐するように変更します。

変数[NumA]と変数[NumB]が一致しているかを比較して、その結果を[Branch]ノードの[Condition]ピンに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-17-50.png)

比較演算子ノードを追加する時は、比較演算子で検索し、図のノードコメントをメニューから選択します。
後ほど、比較演算子の一覧を載せましたので有効活用してください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-15-08-50.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-24-04.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

計算結果のPrintStringが出力されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-19-56.png)

変数[NumA]の値は[1]、変数[NumB]の値は[2]なので、一致しません。
[Branch]ノードは[False]の実行ピンに処理を切り替えて、計算結果を出力する[PrintString]ノードを実行しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-16-43-53.png)

比較演算子は「一致している（Equal）」以外にも用意されています。
一覧を用意しましたので、有効活用してください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-20-27.png)

| 検索Word | Menu項目      | Blueprint                                                                                            | 数式 | 読み方     | 使い方 | 意味             |
| -------- | ------------- | ---------------------------------------------------------------------------------------------------- | ---- | ---------- | ------ | ---------------- |
| ==       | Equal         | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-27-56.png) | =    | 等しい     | A==B   | AとBは等しい     |
| <        | Less          | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-28-23.png) | <    | 小なり     | A<B    | AはBより小さい   |
| >        | Greater       | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-28-48.png) | ＞   | 大なり     | A>B    | AはBより大きい   |
| <=       | Less Equal    | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-14.png) | ≦    | 以下       | A<=B   | AはB以下         |
| >=       | Greater Equal | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-35.png) | ≧    | 以上       | A>=B   | AはB以上         |
| !=       | Not Equal     | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-57.png) | ≠    | 等しくない | A!=B   | AとBは等しくない |

### 論理演算子ノードで処理を切り替える

変数NumCが「10より大きく、30以下」のような範囲内かどうかで分岐させます。
[AND]と書かれたノードは[AND Boolean]と検索して追加してください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-24-53.png)

「Make Literal Int」は変数を作成せずに、VariableType（変数の型）の値を使いたい時に使用するノードです。
「Make Literal （VariableType）」をメニューから選択します。
「Make Literal （VariableType）」のValueに値を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-36-34.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-24-04.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

「Hello World!」を出力する[PrintString]ノードの処理のみが実行されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-21-36.png)

今回は変数[NumC]に[15]の値が設定されていたので、「10<NumC（15）」と[NumC（15）<30]の条件が両方ともTrueだったので、[AND Boolean]ノードは[True]になります。
[Branch]ノードは[True]の処理に切り替えて、[Hello World!]を出力する[PrintString]ノードを実行しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-18-11-10.png)

[AND Boolean]のように複数の条件を組み合わせて、より複雑な条件を表すときに使うのが**論理演算子**です。
論理演算子は「AND Boolean」以外にも用意されています。
一覧を用意しましたので、有効活用してください。

| 検索Word    | Menu項目    | Blueprint                                                                                            | 読み方     | 使い方         | 意味                |
| ----------- | ----------- | ---------------------------------------------------------------------------------------------------- | ---------- | -------------- | ------------------- |
| AND Boolean | AND Boolean | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-11-11.png) | かつ       | 1<=a&&a<=5 | aは1以上かつ5以下 |
| OR Boolean  | OR Boolean  | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-25-28.png) | または     | a==1\|\|a==2  | Aの値が1または2     |
| Not Boolean | Not Boolean | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-25-50.png) | ～ではない | !(a==1)        | Aは1ではない        |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-22-06-18.png)

論理演算子はこの3種類以外にも用意されています。
興味があれば調べてみてください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-22-24.png)

### 複数の選択肢で分岐する

変数[CalcType]の数値で計算結果を1つだけPrintStringで出力するように変更します。

DefaultValueを変更して、引き算のPrintStringが出力されるように変更します。

| VariableName | VariableType | Category     | DefaultValue |
| ------------ | ------------ | ------------ | ------------ |
| IsPrintHello | Boolean      | Flow Control | false        |
| CalcType     | Integer      | Flow Control | 1            |

図のように[Branch]ノードを追加して処理を切り分けてください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-18-23-06.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-13-24-04.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

引き算の結果が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-25-30.png)

変数[IsPrintString]が[False]なので、最初の[Branch]ノードは[False]の実行ピンを実行します。
次の[Branch]ノードでは、変数[CalcType]と値が一致していないので[False]の実行ピンを実行します。
次の[Branch]ノードでは、変数[CalcType]と値が一致するので、引き算の[PrintString]ノードが実行されます。
[Branch]ノードを複数組み合わせることで、複数の選択肢に分岐できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-18-33-32.png)

### すべて保存

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-26-57.png)
