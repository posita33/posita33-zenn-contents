---
title: "【C++】四則演算（+ - x ÷）"
free: false
---

## 【C++】四則演算（+ - x ÷）

### C++でBlueprintを再現すること

Blueprint版で実装した四則演算の結果をPrintStringで出力する処理をC++で再現します。

- 赤：Add（足し算）ノード
- 黄：Subtract（引き算）ノード
- 緑：Multiply（掛け算）ノード
- 青：Divide（割り算）ノード

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-41-32.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-41-51.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-42-09.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-42-25.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_Calculation」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-43-16.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-44-00.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-23-08-43-09.png)

ClassTypeとClass名を設定します。

| Property   | Value          |
| ---------- | -------------- |
| Class Type | Public         |
| Name       | CPPCalculation |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-45-34.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPCalculation.cpp
- CPPCalculation.h

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-12-18-41-24.png)

開いたファイルを学習する初期状態に修正します。
この後にComponentやConstructionScriptは使用しないので処理を削除してあります。

```cpp:CPPCalculation.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPCalculation.generated.h"

UCLASS()
class CPP_BP_API ACPPCalculation : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FLinearColor(0.0, 0.66, 1.0);

};

```

```cpp:CPPCalculation.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPCalculation.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPCalculation::BeginPlay()
{
	FString Message = "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
}

```

### 変数を宣言する

Blueprint同様にVariableType：Integerの変数を2つ宣言します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| CalcVarA     | int32        | 7            |
| CalcVarB     | int32        | 3            |

```h:CPPCalculation.h
private:
	// 計算用の変数
	int32 CalcVarA = 7;
	int32 CalcVarB = 3;
```

**VariableType：int（整数型）の種類**
BlueprintではVariableTypeに「Integer」を設定しました。
C++ではVariableTypeに「int32」を設定しましたが、同じ範囲をもつVariableTypeです。
C++で使用できるintの種類を表にしました。

| Type   | Byte数 | 範囲（Min）                | 範囲Max                    | Blueprintの型 |
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

まずはAdd（足し算）ノードを再現してみましょう。
CPPCalculation.cpp BeginePlay関数に処理を追記します。


```cpp:CPPCalculation.cpp
#include "Kismet/KismetMathLibrary.h" // 追加
```

```cpp:CPPCalculation.cpp BeginePlay()
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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-41-32.png)

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

```cpp:CPPCalculation.cpp BeginePlay()

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

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

LevelEditorに戻り「CPPCalculation」をViewportに配置します。
Blueprit側のPrintStringが出力されると確認しづらいので、Viewportに配置した「BP_Calculation」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-54-36.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

CalcVarA + CalcVarB（7+3）の結果が正しく出力されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-12-19-06-26.png)

#### 引き算、掛け算、割り算の処理を再現する

それでは足し算以外の四則演算の処理を書いていきましょう。

```cpp:
// C++の四則演算の書き方
CalcVarA + CalcVarB // 足し算
CalcVarA - CalcVarB // 引き算
CalcVarA * CalcVarB // 掛け算
CalcVarA / CalcVarB // 割り算
```

数式に使用する「+」などの文字は「**演算子**」と言います。
「**数式の演算子**」と「**プログラミングの演算子**」では、掛け算と割り算の記号が違います。

| 日本語 | 英語     | 数式の演算子 | プログラミングの演算子 |
| ------ | -------- | ------------ | ---------------------- |
| 足す   | Add      | +            | +                      |
| 引く   | Subtract | -            | -                      |
| 掛ける | Multiply | ×            | *（アスタリスク）      |
| 割る   | Divide   | ÷            | /（スラッシュ）        |

Blueprint以外にもMaterialなど他のEditorでも四則演算ノードが用意されています。
ノードのヘッダ部分に英語が表示されますので、四則演算の英単語を覚えていくと対応できます。

```cpp:CPPCalculation.cpp BeginePlay()
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
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-41-51.png)

```cpp:CPPCalculation.cpp BeginePlay()
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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-42-09.png)

```cpp:CPPCalculation.cpp BeginePlay()
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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-42-25.png)

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

四則演算の結果が正しく表示されました。
Blueprintの時と同様に、割り算の結果が小数点切り捨てになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-12-19-13-50.png)

### 割り算の結果を小数点まで表示させる

割り算の結果が小数点切り捨てになります。
Blueprintでは小数点まで表示させるには変数の型を[Integer]を[Float]に変換することで解決できました。
C++で[int32]から[float]に変換（Cast）することで小数点を扱えます。

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

VariableTypeがint32の変数[CalcVarA],[CalcVarB]の変数型をヘッダーファイルでFloatに変更できます。
一時的に[int32]から[float]に変換（Cast）させる方法は、変数の前に（VariableType）とすることで変換できます。
変換できるVariableTypeと、変換できないVariableTypeがありますので、気を付けて使用してください。

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

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

割り算の結果が小数点まで表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-12-19-18-02.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-03-05-10-58-35.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-12-19-21-00.png)

## BlueprintとC++の処理を並べてみる

BlueprintとC++の処理を並べてみます。
Blueprintで[Sequence]ノードを使うと、処理を上から下に並べられます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-calculation/2022-02-12-20-19-58.png)

## ソースコードとプロジェクト

ここまでのソースコードとプロジェクトファイルをGitHubからダウンロードできます。

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/tree/main/Resources/Chapter_02/Calculation

**CPPCalculation.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Calculation/Source_end/CPP_BP/Public/CPPCalculation.h

**CPPCalculation.cpp**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Calculation/Source_end/CPP_BP/Private/CPPCalculation.cpp
