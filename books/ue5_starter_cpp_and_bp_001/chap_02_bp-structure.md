---
title: "【BP】Structure（構造体）"
free: false
---

## 【Blueprint】Structure（構造体）

### 今回できること

今までの処理をStructure（構造体）を使用した処理に変更します。
Structure（構造体）は異なるVariableTypeの変数を1つにまとめられます。
Array（配列）との違いは、Array（配列）は1つのVariableTypeしか持てませんが、Structure（構造体）は異なるVariableTypeの変数を持つことができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-15-00-04.png)

構造体の作り方について知ることができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-46-35.png)

構造体の設定について知ることができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-00-20.png)

PrintCalcResultのInputをStructer（構造体）に変更することでより処理が見やすくなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-35-22.png)

### 学習用の新規レベル「Chapter_2_Structure」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-23-32.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Structure」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-32-13.png)

### Blueprintを複製する

「BP_FlowControl_Loop」を複製（Ctrl + W）して、「BP_Structure」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-35-51.png)

### Structure（構造体）「FBPCalcInfo」を作成する

Structure（構造体）「FBPCalcInfo」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-04-05-40-37.png)
*コンテンツブラウザの空きスペース右クリック > Blueprints > Structure*

名前を「FBPCalcInfo」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-05-57-43.png)

変数を追加する。
[New Variable]ボタンをクリックすると変数が追加されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-02-04.png)

変数を一覧に書かれている内容で設定します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| Type         | EBPCalcType  | Add          |
| NumA         | Integer      | 7            |
| NumB         | Integer      | 3            |

設定できたら、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-00-20.png)

### Function[PrintCalcResult]を複製してFunction[PrintCalcResultArgStructure]を作成する

「BP_Structure」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-13-21-56-03.png)

Function「PrintCalcResult」のInput側を[FBPCalcInfo]に置き換えたFunction[PrintCalcResultArgStructure]を作成します。

Function「PrintCalcResult」を複製します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-18-39-16.png)
*Function「PrintCalcResult」を右クリック > Duplicate*

名前を[PrintCalcResultArgStructure]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-05-54-24.png)

InputをStructure（構造体）「FBPCalcInfo」を使用するように変更します。

| Input/Output | VariableName | VariableType |
| ------------ | ------------ | ------------ |
| Input        | CalcInfo     | FBPCalcInfo  |
| Input        | Duration     | float        |

[Duration]を「FBPCalcInfo」に入れなかったのは、[Duration]は計算には使わず、PrintStringに使用するための変数だからです。
構造体は「何に使うか」のカテゴリー化ができるとメンバーが決まります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-06-42.png)

### Structure（構造体）を分解する

Inputを変更したので接続がおかしくなってしまいます。
おかしくなってしまった接続を切ります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-21-04.png)

Structure（構造体）のメンバーから値を取得するにはStructure（構造体）を分解します。
Structure（構造体）の分解は2種類あります。

- Structure（構造体）をピンをSplitする
- Break（Structure Name）ノードを追加する

Structure（構造体）ピンをSplitする方法について紹介します。

Structure（構造体）ピンを右クリックして、[Split Struct Pin]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-22-33.png)

「FBPCalcInfo」に設定した変数名のピンが表示され、Structure（構造体）のメンバーにアクセスできます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-25-07.png)

もう1つの分解方法を説明するついでに、元に戻す方法を紹介します。

Structure（構造体）ピンを分解してできた変数ピンを右クリックして、[Recombine Struct Pin]を選択すると、元のStructure（構造体）ピンに戻せます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-13-38-49.png)

もう1つの分解方法「Break（Structure Name）ノードを追加する」を紹介します。

Structure（構造体）ピンをDrag&Dropし、「Break （Structure Name）」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-13-44-50.png)

Structure（構造体）のメンバーにアクセスできるBreakノードが追加されます。
処理を元通りになるように接続を修正します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-13-50-03.png)

Structure（構造体）[FBPCalcInfo]を使用した処理は以下のようになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-13-57-14.png)

今回はStructure（構造体）のメンバーが少なかったので、どちらの分解方法を使用しても大丈夫でした。
Structure（構造体）のメンバーが大量にある場合は、Breakノードで構造体にアクセスした方が見やすいです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-13-56-19.png)

### Function[PrintCalcResultArgStructure]を使用した処理に編集する

Function[PrintCalcResultArgStructure]を使用した処理に編集します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-06-17-13-22.png)

Function[PrintCalcResultArgStructure]をEventGraphに追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-04-14.png)

インプットのStructure（構造体）ピンへ変数を作成せずに値を設定する方法は分解する方法と同じで2種類あります。

- Structure（構造体）ピンをSplitする
- Make（Structure Name）ノードを追加する

「Structure（構造体）ピンをSplitする」方法については分解する手順と同じです。
Structure（構造体）ピンを右クリックし、[Split Struct Pin]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-13-14.png)

元に戻すには、ピンを右クリックし、[Recombine Struct Pin]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-23-12.png)

「Make（Structure Name）ノードを追加する」についてもBreakノードを追加した時と同じです。
Structure（構造体）ピンからDrag&Dropし、メニューから[Make （Structure Name）]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-18-54.png)

Function[PrintCalcResultArgStructure]を使用した処理に接続を修正します。
Function[PrintCalcResult]は削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-32-25.png)

Inputが整理されて構造体化されることで、ピンに設定する項目が分かりやすくなりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-35-22.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-39-07.png)

Level Editorに戻り、「BP_Structure」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-13-22-01-55.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[C]キーをPressするとFunction[PrintCalcResultArgStructure]はFunction[PrintCalcResult]と同様の処理を行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-42-52.png)

### Structure（構造体）の配列を使った処理に修正する

Structure（構造体）もArray（配列）として宣言できます。

| VariableName | VariableType         | Category     | DefaultValue |
| ------------ | -------------------- | ------------ | ------------ |
| CalcInfos    | FBPCalcInfo（Array） | Flow Control | 0            |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-06-17-12-33.png)

Default Valueを設定するために[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-06-17-27-39.png)

Default Valueを一覧の値になるように設定します。

| Index | Type     | NumA | NumB |
|-------|----------|------|------|
| [0]   | Add      | 7    | 3    |
| [1]   | Subtract | 7    | 3    |
| [2]   | Multiply | 7    | 3    |
| [3]   | Divide   | 7    | 3    |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-06-17-15-07.png)

Structure（構造体）の配列をGet(a ref)で取得するように修正します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-06-17-19-33.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-39-07.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[C]キーをPressするとFunction[PrintCalcResultArgStructure]はFunction[PrintCalcResult]と同様の処理を行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-14-42-52.png)

### すべて保存

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-13-22-06-03.png)

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Variables/Structs/
