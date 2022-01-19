---
title: "2.6.c++ 四則演算(+ - x ÷)"
emoji: "⚙️"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---

## 【C++版】c++ 四則演算(+ - x ÷)

### VisualStudioを開いて、編集するファイルを表示する

プロジェクトを閉じていたら、プロジェクトを開き、
「Chapter_2_7_Calculation」を開きます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-45-05.png)

ToolsからVisual Studioを開きます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-50-21.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPSampleActor.cpp
- CPPSampleActor.h

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-51-04.png)

### C++でBlueprintの四則演算を再現する

Blueprint版で実装した四則演算の結果をPrintStringで出力する処理をC++で再現します。
- 赤：Add(足し算)ノード
- 黄：Subtract(引き算)ノード
- 緑：Multiply(掛け算)ノード
- 青：Divide(割り算)ノード

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-57-14.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-57-30.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-57-48.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-43-43.png)

### 変数を宣言する
Blueprint同様にVariableType：Integerの変数を二つ宣言します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| CalcVarA     | int32        | 7            |
| CalcVarB     | int32        | 3            |


```h:CPPSampleActor.h
private:
	// 計算用の変数
	int32 CalcVarA = 7;
	int32 CalcVarB = 3;
```

**VariableType：int（整数型）の種類**
BlueprintではVariableTypeに「Integer」を設定しました。
C++ではVariableTypeに「int32」を設定しましたが、同じ範囲をもつVariableTypeです。
C++で使用できるintの種類を表にしました。

| Type   | Byte数 | 範囲(Min)                  | 範囲Max                    | Blueprintの型 |
| ------ | ------ | -------------------------- | -------------------------- | ------------- |
| int8   | 1      | -128                       | 128                        | -             |
| uint8  | 1      | 0                          | 255                        | Byte          |
| int16  | 2      | -32,768                    | 32,767                     | -             |
| uint16 | 2      | 0                          | 65,535                     | -             |
| int    | 4      | -2,147,483,648             | 2,147,483,647              | Integer       |
| int32  | 4      | -2,147,483,648             | 2,147,483,647              | Integer       |
| uint32 | 4      | 0                          | 4,294,967,295              | -             |
| int64  | 8      | -9,223,372,036,854,770,000 | 9,223,372,036,854,770,000  | Integer64     |
| uint64 | 8      | 0                          | 18,446,744,073,709,500,000 | -             |


```cpp
1Byte = 8bit
intの右側の数値から8で割るとByte数が出ます。

例) int32は 32/8 = 4(Byte)

±(プラスマイナス)かどうかを決めるためには、1bitが必要です。
先頭のuはunsigned(符号無し)の意味で
－(マイナス)かどうかの1bitを数値のために使うため、最大値が大きくなり、最小値は0になります。
```

### 四則演算の処理を再現する
#### 足し算の処理を再現する
まずはAdd(足し算)ノードを再現してみましょう。
CPPSampleActor.cpp BeginePlay関数に処理を追記します。

```cpp:CPPSampleActor.cpp BeginePlay()
	// Add(足し算)の処理
	int32 ResultAdd = UKismetMathLibrary::Add_IntInt(CalcVarA,CalcVarB);
	FString StrResultAdd = Conv_IntToString(ResultAdd);
	UKismetSystemLibrary::PrintString(
		this
		, StrResultAdd 
		, true
		, true
		, FColor::Red
		, Duration);
```

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-57-14.png)

[Add]ノードは「KismetMathLibrary.h」で[Add_IntInt]関数として宣言されています。
Blueprintを再現するので、使用するには「KismetMathLibrary.h」をincludeします。
```cpp
#include "Kismet/KismetMathLibrary.h" // 追加

	int32 ResultAdd = UKismetMathLibrary::Add_IntInt(CalcVarA,CalcVarB);
```

「KismetMathLibrary.h」の[Add_IntInt]関数を見てみましょう。
```cpp:KismetMathLibrary.h
	/** Addition (A + B) */
	UFUNCTION(BlueprintPure, meta=(DisplayName = "int + int", CompactNodeTitle = "+", Keywords = "+ add plus", CommutativeAssociativeBinaryOperator = "true"), Category="Math|Integer")
	static int32 Add_IntInt(int32 A, int32 B = 1);
```

「KismetMathLibrary.ini」で処理が実装されています。
実際に行っていることは「A + B」です。
```cpp:KismetMathLibrary.ini
KISMET_MATH_FORCEINLINE
int32 UKismetMathLibrary::Add_IntInt(int32 A, int32 B)
{
	return A + B;
}
```

[Add_IntInt]関数を使用しないで書いてみましょう。
```cpp
	int32 ResultAdd = UKismetMathLibrary::Add_IntInt(CalcVarA,CalcVarB);
       ↓
	int32 ResultAdd = CalcVarA + CalcVarB;
```

[Conv_IntToString]関数でint32からFStringに変換しています。
こちらも[Conv_IntToString]関数を使わずに書いてみましょう。
```cpp
//Conv_IntToString()を使用するにはincludeの追加が必要です
#include "Kismet/KismetStringLibrary.h"

	FString StrResultAdd = Conv_IntToString(ResultAdd);

//Conv_IntToString()のint32 > FString変換処理
	FString::Printf(TEXT("%d"), InInt);	
```

PrintString関数以外は、Blueprintで使用したノードを使用しない書き方です。

```cpp:CPPSampleActor.cpp BeginePlay()

	// Add(足し算)の処理
	int32 ResultAdd = CalcVarA + CalcVarB;
	FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
	UKismetSystemLibrary::PrintString(
		this
		, StrResultAdd 
		, true
		, true
		, FColor::Red
		, Duration);

```
Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-29-32.png)

LevelEditorに戻り「CPPSampleActor」をViewportに配置します。
Blueprit側のPrintStringが出力されると確認しづらいので、Viewportに配置した「BP_SampleActor」を削除します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-27-37.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-30-37.png)

CalcVarA + CalcVarB（7+3）の結果が正しく出力されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-34-06.png)

#### 引き算、掛け算、割り算の処理を再現する

それでは足し算以外の四則演算の処理を書いていきましょう。

```cpp:
// C++の四則演算の書き方
CalcVarA + CalcVarB // 足し算
CalcVarA - CalcVarB // 引き算
CalcVarA * CalcVarB // 掛け算
CalcVarA / CalcVarB // 割り算
```
数学記号とプログラミング記号では、掛け算と割り算の記号が違います。
| 日本語 | 英語     | 数学記号 | プログラミング記号 |
| ------ | -------- | -------- | ------------------ |
| 足す   | Add      | +        | +                  |
| 引く   | Subtract | -        | -                  |
| 掛ける | Multiply | ×        | *(アスタリスク)    |
| 割る   | Divide   | ÷        | /(スラッシュ)      |

Blueprint以外にもMaterialなど他のEditorでも四則演算ノードが用意されています。
ノードのヘッダ部分に英語が表示されますので、四則演算の英単語を覚えていくと対応することが意味が分かります。


```cpp:CPPSampleActor.cpp BeginePlay()
	// Subtract(引き算)の処理
	int32 ResultSubtract = CalcVarA - CalcVarB;
	FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
	UKismetSystemLibrary::PrintString(
		this
		, StrResultSubtract
		, true
		, true
		, FColor::Yellow
		, Duration);
```
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-57-30.png)

```cpp:CPPSampleActor.cpp BeginePlay()
	// Multiply(掛け算)の処理
	int32 ResultMultiply = CalcVarA * CalcVarB;
	FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
	UKismetSystemLibrary::PrintString(
		this
		, StrResultMultiply
		, true
		, true
		, FColor::Green
		, Duration);
```
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-07-57-48.png)

```cpp:CPPSampleActor.cpp BeginePlay()
	// Divide(割り算)の処理
	int32 ResultDivide = CalcVarA / CalcVarB;
	FString StrResultDivide = FString::Printf(TEXT("%d"), ResultDivide);
	UKismetSystemLibrary::PrintString(
		this
		, StrResultDivide
		, true
		, true
		, FColor::Blue
		, Duration);

```
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-43-43.png)


Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-29-32.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-30-37.png)

四則演算の結果が正しく表示されました。
Blueprintの時と同様に、割り算の結果が小数点切り捨てになります。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-51-59.png)

### 割り算の結果を小数点まで表示させる
割り算の結果が小数点切り捨てになります。
Blueprintでは小数点まで表示させるには変数の型を[Integer]を[Float]に変換することで解決できました。
C++で[int32]から[float]に変換（Cast）させて小数点を扱うことが出来る処理です。

```cpp:.cpp
	// Divide(割り算)の処理(int > float)
	float ResultDivide = (float)CalcVarA / (float)CalcVarB;
	FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
	UKismetSystemLibrary::PrintString(
		this
		, StrResultDivide
		, true
		, true
		, FColor::Blue
		, Duration);
```

VariableTypeがint32の変数[CalcVarA],[CalcVarB]の変数型をヘッダーファイルでFloatに変更することもできます。
一時的に[int32]から[float]に変換（Cast）させる方法は、変数の前に（VariableType）とすることで変換できます。
出来るVariableTypeと出来ないVariableTypeがありますので、気を付けて使用してください。
```cpp
int32 ResultDivide = CalcVarA / CalcVarB;
  ↓
float ResultDivide = (float)CalcVarA / (float)CalcVarB;
```

少数点を含む文字列をFStringに変換するには、「%d」から「%f」に変更します。
```cpp
FString::Printf(TEXT("%d"), ResultDivide);
  ↓
FString::Printf(TEXT("%f"), ResultDivide);
```

フォーマット指定子といって、「%英字1文字」の部分を、引数に渡した変数で置き換えてくれます。
変数の型によって、「半角英字1文字」の部分を変更します。
https://www.k-cube.co.jp/wakaba/server/format.html


Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-29-32.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-09-30-37.png)

割り算の結果が小数点まで表示されます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-19-14-23-15.png)

### 全てを保存して、C++側の説明は終了です
C++側の説明は以上になります。
プロジェクトを全て保存しましょう。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-20-06-03-35.png)

## BlueprintとC++の処理を並べてみる
BlueprintとC++の処理を並べてみます。
Blueprintで[Sequence]ノードを使うと、処理を上から下に並べることが出来ます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-01-20-06-19-13.png)




