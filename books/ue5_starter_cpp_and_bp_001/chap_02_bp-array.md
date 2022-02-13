---
title: "【BP】Array（配列）"
free: false
---

## 【Blueprint】Array（配列）

### 今回できること

変数をArray（配列）に変更します。
Array（配列）は同じVariableTypeを複数持つことができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-05-18-21-43.png)

Array（配列）の設定方法や取得について解説します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-59-46.png)

Array（配列）の取得でよく使用する2つの方法について解説します。

- Array（配列）をランダムに取得する。
- Array（配列）を剰余（％）を使用して順番に取得する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-58-55.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-50-57.png)


### 学習用の新規レベル「Chapter_2_Array」を作成する

学習用の新規レベルを作成します。
[File]メニューから[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-21-51-56.png)

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-21-52-05.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-21-52-15.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Array」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-21-54-06.png)

### Blueprintを複製する

「BP_EventDispatchcer」を複製（Ctrl + W）して、「BP_Array」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-52-59.png)

### 変数[Message]を配列の変数[Messages]に変更する

「BP_Array」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-13-21-04-39.png)

変数[Message]を配列の変数[Messages]に変更します。

変数[Message]を選択し、Variable Nameを[Messages]に変更します。配列の変数を宣言する時は複数形の名前にすると配列ということが分かりやすくなります。
Variable Typeの右端のアイコンをクリックし、[Array（配列）]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-59-46.png)

Variable TypeをArray（配列）に変更すると、変数をEvent Graphで使用しているので確認ダイアログが表示されます。[Change Variable Type]をクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-30-10.png)

[My Blueprint]パネルの変数[Messages]のVariable Typeのアイコンが変わっています。アイコンを確認することで変数が配列か判別できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-31-43.png)

### 変数[Messages]にDefault Valueを設定する

変数[Messages]にDefault Valueを設定します。
Default Valueを設定するので、[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-19-32.png)

Array（配列）はDefault Valueの設定方法が変わります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-23-01.png)

Default Valueの[+]ボタンをクリックすると設定できる要素が増えます。
以下の表の国ごとの"Hello World!"を内容をDefault Valueに設定します。
配列の数え方は[0]が1番目になります。

| Index | Value             |
| ----- | ----------------- |
| [0]   | Hello World!      |
| [1]   | 你好 世界!        |
| [2]   | Bonjour le monde! |
| [3]   | Hallo Welt!       |
| [4]   | こんにちは世界!   |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-36-09.png)

### 変数[Messages]から値を取得する

変数[Messages]から値を取得します。

Variable Typeを変更したので、変数[Messages]のGetノードでエラーが発生しています。エラーとなっているピンの接続を切断します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-33-13.png)

変数[Messages]のGetノードからDrag&Dropし、[Get（a ref）]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-35-34.png)

Array（配列）のGetノードには[Get(a ref)]と[Get(a copy)]の2種類があります。
Function（関数）で説明した「参照渡し」と「値渡し」でArray（配列）の値を取得するかの違いです。

- Get(a ref)：参照渡しで値を取得します。
- Get(a copy)：値渡しで値を取得します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-48-28.png)

日本語の"こんにちは世界!"を取得するように、Getノードの数値には[4]を設定します。
Getノードを[Print String]ノードの[In String]に接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-38-45.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-40-12.png)

Level Editorに戻り、「BP_Array」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-13-18-48-34.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-23-14-00.png)

[H]キーをPressすると、変数[Messages]のIndex[4]に設定した文字列が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-23-16-07.png)


### 変数[Messages]からランダムに値を取得する

変数の取得方法についてよく使う方法を2つ紹介します。

まずは、変数[Messages]からランダムに値を取得する方法です。

メニューから[Random Integer in Range]を選択します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-42-17.png)

[Random Integer in Range]の[Max]ピンに配列の最後のIndex Noである[4]を設定します。
[Random Integer in Range]の[Return Value]ピンとGetノードを接続します。

配列は[0]から始まるので、Index NoのMaxは「配列数 - 1」になります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-45-10.png)

[compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-06-27-58.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-23-14-00.png)

[H]キーをPressすると、変数[Messages]の文字列がランダムに表示されます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-06-38-46.png)

配列数が変わっても処理を変えずに済むように変更します。

変数[Messages]からDrag&Dropし、[Length]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-48-25.png)

[Length]のアウトプットピンからDrag&Dropし、[Subtract（-）]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-50-55.png)

[Subtract]のアウトプットピンを[Random Integaer in Range]の[Max]ピンに接続します。
配列は[0]から始まるので、Index NoのMaxは「配列数 - 1」になります。
配列の数を増やしても処理を変えずにMaxの値を取得できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-55-40.png)

[compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-06-27-58.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-23-14-00.png)

[H]キーをPressすると、先ほどと同じように配列の文字列をランダムに取得できます。配列数が変わってもMaxの値を変更せずに済むので[Length]ノードを使用した取得は便利です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-58-55.png)

配列からRandomのElementとIndexを取得できるRandom関数があります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-06-12-01-04.png)

Random関数から取得できるElementは値渡しになるので、参照渡しにしたい場合はRandom関数のIndexをGet（a ref）に渡して取得します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-06-11-56-34.png)

### 変数[CalcType]を配列の変数[CalcTypes]に変更する

次に、剰余（％）を使用して、順番に配列を取得する方法について説明します。

Index番号を保持するための変数[TypeIndex]を宣言します。

| VariableName | VariableType | Category     | DefaultValue |
| ------------ | ------------ | ------------ | ------------ |
| TypeIndex    | Integer      | Flow Control | 0            |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-13-18-55-51.png)

変数[CalcType]を選択し、Variable Nameを[CalcTypes]に変更します。
Variable Typeの右端のアイコンをクリックし、[Array（配列）]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-13-18-58-18.png)

Default Valueを設定するので、[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-06-27-58.png)

変数[CalcTypes]のDefault Valueを設定します。

| Index | Value    |
| ----- | -------- |
| [0]   | Add      |
| [1]   | Subtract |
| [2]   | Multiply |
| [3]   | Divide   |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-16-50.png)

### 変数[CalcTypes]の値を順番に取得して出力する

変数[CalcTypes]の値を順番（[0:Add]> [1:Subtract] > [2:Multiply] > [3:Divide] > [0:Add] > 繰り返し）に出力するように処理を編集します。

Variable Typeを変更したのでエラーになっているピンの接続を切断します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-19-25.png)

変数[CalcTypes]の値を変数[TypeIndex]で取得します。

先ほど追加した変数[TypeIndex]のGetを追加します。
変数[TypeIndex]のGetノードと変数[CalcTypes]のGetを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-27-58.png)

Function[PrintCalcResult]実行後に、TypeIndexをIncrementします。

Incrementは変数の値を[+1]してくれるノードです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-33-15.png)

Increamentをして[+1]した変数[TypeIndex]の値をループする計算を追加します。

「％」は割り算の余り（剰余）を取得できるノードです。

「7 ÷ 3 = 2 余り1」の「余り1」を取得できます。

現在のIndex ÷ Length（配列数）の余りを求めると、配列のIndexをオーバーすることがなくなります。

「4 ÷ Length（4） = 1 余り0」になるので、配列数とIndexが同じになっても、配列のIndexをオーバーせずに最初の[0]に戻せます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-43-13.png)

実行回数が配列数を越えるように実行した時の変数[TypeIndex]の値を表にしました。
[[3]:Divide]実行後、[[0]：Add]に戻って繰り返します。

| 実行回数 | Get時のTypeIndexの値 | CalcTypeResultのType | TypeIndex ++ | Length ％ TypeIndex | 最終的なTypeIndexの値 |
|------|------------------|---------------------|--------------|------------------|-----------------|
| 1    | 0                | [0]：Add             | 1            | 4%1              | 1               |
| 2    | 1                | [1]：Subtract        | 2            | 4%2              | 2               |
| 3    | 2                | [2]：Multiply        | 3            | 4%3              | 3               |
| 4    | 3                | [3]：Divide          | 4            | 4%4              | 0               |
| 5    | 0                | [0]：Add             | 1            | 4%1              | 1               |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-44-53.png)

[compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-06-27-58.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-23-14-00.png)


[C]キーをPressすると、変数[CalcTypes]の値を順番（[0:Add]> [1:Subtract] > [2:Multiply] > [3:Divide] > [0:Add] > 繰り返し）に出力します。

現在のIndex ÷ Length（配列数）の余りを現在のIndexに設定する処理はif文で最大数を比較しなくて済むのでスマートな書き方になります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-50-57.png)

### すべて保存

Blueprint側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-02-13-19-05-12.png)

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Arrays/

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/BP_HowTo/WorkingWithArrays/
