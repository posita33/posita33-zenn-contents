---
title: "【BP】 四則演算(+ - x ÷)"
emoji: "⚙️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---

## 【Blueprint】四則演算（+ - x ÷）

「**四則演算**」という難しい名前を使用しましたが、「**足し算**」「**引き算**」「**掛け算**」「**割り算**」のことです。

UE5から四則演算のノードの使用方法が変わります。
よく使用するノードなので、このタイミングで覚えてしまいましょう。

### 今回できること

Blueprintで四則演算ノードを使用して、PrintStringで計算結果を出力します。

数式に使用する「+」などの文字は「**演算子**」と言います。
「**数式の演算子**」と「**プログラミングの演算子**」では、掛け算と割り算の記号が違います。
プログラミングをする際に覚えておくと役に立つのが、英語にしたときの動詞とプログラミングの演算子です。
ノードを追加するときや、コードを見るときに役に立ちます。

| 日本語 | 英語     | 数式の演算子 | プログラミングの演算子 |
| ------ | -------- | -------- | ------------------ |
| 足す   | Add      | +        | +                  |
| 引く   | Subtract | -        | -                  |
| 掛ける | Multiply | ×        | *（アスタリスク）    |
| 割る   | Divide   | ÷        | /（スラッシュ）      |

### 学習用の新規レベル「Chapter_2_7_Calculation」を作成する

学習用の新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-07-32-48.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-01-26-22-32-19.png)

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-07-33-00.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_7_Calculation」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-07-35-22.png)

### 計算に使用する変数を追加する

「**BP_SampleActor**」をBlueprint Editorで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-07-51-11.png)

四則演算ノードの計算で使用する変数を追加します。
今回は**FloatとInegerの違いを説明するため**に、**VariableTypeをInteger**(**整数**)に設定します。

| VariableName | VariableType | Category    | DefaultValue |
|--------------|--------------|-------------|--------------|
| CalcVarA     | Integer      | Calculation | 7            |
| CalcVarB     | Integer      | Calculation | 3            |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-07-46-23.png)

### 四則演算ノードの追加手順

`CalcVarA + CalcVarB`の結果をPrintStringで出力します。

$$
CalcVarA + CalcVarB
$$

変数[CalcVarA],[CalcVarB]のGetノードを追加し、PrintStringノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-15-08-37.png)

変数[CalcVarA]のGetノードからDrag&Dropし、[**+（プラス）**]で検索します。
メニューから[**Add**]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-17-55.png)

[PrintString]ノードの[In String]が[Add]ノードのOutputピンになるように接続します。
[PrintString]ノードの[Duratin]は変数[Duration]のGetノードを追加して接続します。
[PrintString]ノードの[TextColor]は赤を設定します。
[PrintString]ノード同士を実行ピンで接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-26-47.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-22-19.png)

Level Editorに戻り、Viewportに「**BP_SampleActor**」をDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-29-02.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-29-46.png)

赤い文字列がAddノードの計算結果です。

$$
CalcVarA（7） + CalcVarB（3） = 10
$$

足し算の計算結果がただしく行われています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-31-04.png)

### その他の四則演算ノードの追加

その他の四則演算「**引き算（-）**」「**掛け算（×）**」「**割り算（÷）**」の結果をPrintStringで出力します。

**引き算**

$$
CalcVarA（7） - CalcVarB（3） = 4
$$

**掛け算**

$$
CalcVarA（7） × CalcVarB（3） = 21
$$

**割り算は割り切れないので小数点がある数値になります**

$$
CalcVarA（7） \div CalcVarB（3） = 2.333...
$$


「**BP_SampleActor**」をBlueprint Editorで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-07-51-11.png)


足し算の処理を範囲選択して、Copy&Pasteします。
[Add]ノードを削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-43-27.png)


[**Subtract（引き算）**]ノードを追加します。
CalcVarAからDrag&Dropし、[**-（マイナス）**]で検索します。
メニューから[**Subtract**]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-45-58.png)

[**Subtract（引き算）**]ノードのOutputピンを[PrintString]ノードの[InString]ピンに接続します。
[PrintString]ノードの[TextColor]ピンには「黄色」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-20-49.png)


[**Multiply（掛け算）**]ノードを追加します。
[**Subtract（引き算）**]ノードを追加手順と同様に範囲選択してCopy&Pasteし、四則演算ノードを削除します。
CalcVarAからDrag&Dropし、[**\*（アスタリスク）**]で検索します。プログラミング言語の掛け算は[**\*（アスタリスク）**]を使用します。
メニューから[**Multiply**]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-04-46.png)

[**Multiply（掛け算）**]ノードのOutputピンを[PrintString]ノードの[InString]ピンに接続します。
[PrintString]ノードの[TextColor]ピンには「緑」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-25-52.png)

[**Divide（割り算）**]ノードを追加します。
[**Subtract（引き算）**]ノードを追加手順と同様に範囲選択してCopy&Pasteし、四則演算ノードを削除します。
CalcVarAからDrag&Dropし、[**/（スラッシュ）**]で検索します。プログラミング言語の割り算は[**/（スラッシュ）**]を使用します。
メニューから[**Divide**]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-06-44.png)

[**Divide（割り算）**]ノードのOutputピンを[PrintString]ノードの[InString]ピンに接続します。
[PrintString]ノードの[TextColor]ピンには「水色」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-27-24.png)

四則演算ノード「**足し算（+）**」「**引き算（-）**」「**掛け算（×）**」「**割り算（÷）**」をPrintStringで出力するBlueprintです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-31-52.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-22-19.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-29-46.png)

四則演算ノードのそれぞれの結果は合っています。
しかし、割り算の小数点が切り捨てられてしまいました。
割り算の結果を小数点まで表示するように修正します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-17-36-49.png)


### 割り算の結果に小数点も表示する

割り算の結果を小数点まで表示されなかったのは、VariableType（整数の型）に問題があります。

[**Divide（割り算）**]ノードのOutputピンのVariableType（整数の型）はIntegerです。

**Integer（整数型）**：整数しか持てないので、小数点の数値は切り捨てられます。

$$
CalcVarA（7） \div CalcVarB（3） = 2（Integer:整数）
$$

**Float（浮動小数点型）**：小数点が持てるので、小数点も保持できます。

$$
CalcVarA（7） \div CalcVarB（3） = 2.333...（Float:小数点）
$$

[**Divide（割り算）**]ノードのOutputピンをIntegerからFloatに変更します。
この昨日はUE5から実装される予定の機能です。
UE4では型ごとに四則演算ノードが用意されていました。

**UE5からはピンの型を変更できます。**

[Divide]ノードのOutputピンを右クリックし、「Convert Pin... > Float」と選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-03-27.png)

[**Divide（割り算）**]ノードのOutputピンから再び、[PrintString]ノードの[InString]ピンに接続します。
[Integer]から[String]に変換するノードは使用しないので削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-05-01.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-22-19.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-29-46.png)

出力された文字列を確認すると、小数点まで表示されています。
数値を扱うときはVariableType（変数の型）を意識しないと、意図しない数値になってしまいます。

1個、2個と数えられる数値は「Integer」
1メートル10センチ10ミリみたいな単位の数値は「Float」

何を変数に設定するかでVariableTypeに気を付けましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-10-17.png)


### MathExpressionノードで数式を書く

数学に詳しく、数式で書きたい人用に、[MathExpression]ノードが用意されています。

EventGraphを右クリックし、メニューから[Add Math Expression]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-22-32.png)

[Math Expression]ノードを選択し、[Expression]プロパティのテキストボックスに[（A + B）]という足し算の数式を書きます。

数式内のA,Bという文字列はInputピンに変換されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-25-48.png)

PrintStringノードでOutputピンの値を出力するように処理を修正します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-34-52.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-22-19.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-16-29-46.png)

[MathExpression]ノードのOutputピンの数値が出力されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-18-41-28.png)

[MathExpression]ノードをダブルクリックすると、文字列からノードが作られています。
すごい機能ですね。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-calculation/2022-01-18-19-56-12.png)

使えない数式もありますので、使用する際には公式ドキュメントをご確認ください。

https://docs.unrealengine.com/4.27/ja/RenderingAndGraphics/Materials/ExpressionReference/Math/
