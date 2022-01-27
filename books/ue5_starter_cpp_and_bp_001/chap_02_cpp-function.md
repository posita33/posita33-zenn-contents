---
title: "【C++】 関数(Function)"
emoji: "📌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp", "unrealengine", "ue4", "ue5"]
published: false
---

## 【C++】関数（Function）

### C++でBlueprintを再現すること

Blueptintの[Add]ノードを再現するFunction[Sum]を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-03-20.png)

Blueptintのローカル変数を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-10-06-42.png)

C++では「値渡し」と「参照渡し」に違いについて説明します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-17-45-39.png)


Blueptintの計算結果の出力処理するFunction[PrintCalcResult]を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-03-31.png)


### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、
「Chapter_2_Function」を開きます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-30-29.png)

[Tools]メニューから[New C++ Class]を開きます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-31-47.png)

親クラスに[Actor]を選択します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-32-21.png)

ClassTypeとClass名を設定します。

| Property   | Value       |
| ---------- | ----------- |
| Class Type | Public      |
| Name       | CPPFunction |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-37-35.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPFunction.h
- CPPFunction.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-07-53-18.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPFunction.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPCalcType.h"
#include "CPPFunction.generated.h"

UCLASS()
class CPP_BP_API ACPPFunction : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FColor(255, 255, 255);

	// 計算用の変数
	int32 CalcVarA = 7;
	int32 CalcVarB = 3;

	// Flow Control用の変数
	bool IsPrintHello = false;
	ECPPCalcType CalcType = ECPPCalcType::Subtract;

};

```

```cpp:CPPFunction.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPFunction.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPFunction::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	if (IsPrintHello)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		switch (CalcType)
		{
			case ECPPCalcType::Add:
			{
				// Add(足し算)の処理
				int32 ResultAdd = CalcVarA + CalcVarB;
				FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
				UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
				break;
			}
			case ECPPCalcType::Subtract:
			{
				// Subtract(引き算)の処理
				int32 ResultSubtract = CalcVarA - CalcVarB;
				FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
				UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, Duration);
				break;
			}
			case ECPPCalcType::Multiply:
			{
				// Multiply(掛け算)の処理
				int32 ResultMultiply = CalcVarA * CalcVarB;
				FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
				UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, Duration);
				break;
			}
			case ECPPCalcType::Divide:
			{
				// Divide(割り算)の処理(int > float)
				float ResultDivide = (float)CalcVarA / (float)CalcVarB;
				FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
				UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, Duration);
			}
		}
	}
}

```

### Function[Sum]を作成する

C++では関数のひな形となる「**プロトタイプ**」をヘッダーファイル（.h）で宣言します。

```cpp:CPPFunction.h
public:
	int32 Sum(int32 A, int32 B);
```
プロトタイプは処理を書かずに、Functionがどのような作りか説明します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-18-09-39.png)

Blueprintの[Detail]パネルで設定した内容と一緒です。


| Input/Output | VariableName | VariableType | C++                     |
| ------------ | ------------ | ------------ | ----------------------- |
| Input        | A            | Integer      | int32 A （第1引数）     |
| Input        | B            | Integer      | int32 B （第2引数）     |
| Output       | ReturnValue  | Integer      | int32（戻り値の型だけ） |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-10-01-43.png)


CPPFunction.cppにFunction[Sum]を定義します。
Visual Studioの機能で、Function名にカーソルを合わせて、「▼」をクリックするとメニューが表示されます。
メニューから[Create Inplementation]を選択すると、「CPPFunction.cpp」に関数の定義が追加されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-08-10-23.png)

「CPPFunction.cpp」に定義されたFunction[Sum]を引数[A],[B]で足し算をするように編集します。

```cpp:CPPFunction.cpp
int32 ACPPFunction::Sum(int32 A, int32 B)
{
	return A + B;
}
```
BlueprintとC++のFunction[Sum]を横に並べてみましょう。
お互いの共通部分を矢印で示すと、Function[Sum]何をしているのか分かりやすくないですか？

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-10-05-13.png)

BlueprintとC++では以下のような関係性を持っています。

| Blueprint    | C++          |
| ------------ | ------------ |
| Grapth       | .cppファイル |
| Detailパネル | .hファイル   |


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-08-41-18.png)

### Function[Sum]を使用する

「プロトタイプ」「関数の定義」ができたので、Function[Sum]を使用します。
変数[CalcVarA]と[CalcVarB]の足し算をFunction[Sum]を使用するように変更します。


```cpp
int32 ResultAdd = CalcVarA + CalcVarB;
   ↓
int32 ResultAdd = Sum(CalcVarA,CalcVarB);
```


```cpp:CPPFunction.cpp BeginPlay()
case ECPPCalcType::Add:
{
	// Add(足し算)の処理
	int32 ResultAdd = Sum(CalcVarA, CalcVarB);
	FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
	UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
	break;
}
```

switch文のAddの分岐に入るため、「CPPFunction.h」に宣言されている変数[CalcType]の値を[ECPPCalcType::Add]に変更します。
```cpp:CPPFunction.h
	ECPPCalcType CalcType = ECPPCalcType::Subtract;
        ↓
	ECPPCalcType CalcType = ECPPCalcType::Add;
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-13-31.png)

「CPPFunction」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_Function」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-17-13.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-17-33.png)

Function[Sum]が実行され、足し算の計算結果が出力されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-25-43.png)

### Function内でのみ使用できるLocal Variable（ローカル変数）を宣言する

BlueprintではFunction内でしか使用できない「**Local Variable（ローカル変数）**」を説明しました。
C++でローカル変数を使用した処理を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-10-06-42.png)


```cpp:CPPFunction.cpp Sum()
int32 ACPPFunction::Sum(int32 A, int32 B)
{
	int32 LocalResult = A + B;
	return LocalResult;
}
```

Local Variable「LocalResult」をBeginPlayで使用するように書きます。
コンパイルすると「undeclared identifier（宣言されていない識別子）」として扱われます。
C++でもローカル変数は関数内でしか使用できません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-10-15-30.png)

C++ではローカル変数を自由に宣言できます。
次のように処理を書いてコンパイルします。

```cpp
int32 VarA = 1;

if(VarA==1)
{
    int32 VarB = varA;
}

int32 VarC = VarB;
```

ローカル変数[VarB]は「undeclared identifier（宣言されていない識別子）」として扱われます。
変数が有効な範囲のことを「**スコープ**」と呼びます。
C++ではif文の{}（ブロック）内も変数のスコープとなり、｛｝内で宣言されたローカル変数は｛｝内でしか使用できません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-10-23-57.png)

スコープについては以下のURLの説明が分かりやすかったです。
GitHubで【ゼロから学ぶC++】が公開されています。
C++に関して詳しく説明されているので、興味がある方はこちらも閲覧してみてはいかがでしょうか。

https://rinatz.github.io/cpp-book/ch04-03-scopes/


### 値渡しと参照渡し

エンジンソースを読んでいると、引数の型に「＆」が付いているFunctionをよくみかけます。
「**参照渡し**」と呼ばれる書き方です。
「＆」がついていない書き方は「**値渡し**」と呼ばれます。
「**参照渡し**」と「**値渡し**」の違いについて解説します。

参照渡しのFunction[SumRef]のプロトタイプを「CPPFunction.h」に宣言します。

```cpp:CPPFunction.h
public:
	int32 SumRef(int32& A, int32& B);
```

参照渡しのFunction[SumRef]の定義を「CPPFunction.cpp」に実装します。

```cpp:CPPFunction.cpp SumRef()
int32 ACPPFunction::SumRef(int32& A, int32& B)
{
	return A + B;
}
```

足し算の計算結果出力を参照渡しのFunction[SumRef]を使用した書き方に変更します。

```cpp:CPPFunction.cpp BeginPlay()
case ECPPCalcType::Add:
{
    // Add(足し算)の処理
    int32 ResultAdd = SumRef(CalcVarA, CalcVarB);
    FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
    UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
    break;
}
```

Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-13-31.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-17-33.png)

値渡しのFunction[Sum]と参照渡しのFunction[SumRef]は同じ結果を出力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-25-43.png)


何が違うのでしょうか？

値渡しのFunction[Sum]と、参照渡しのFunction[SumRef]内で、引数[A],[B]の値を変更します。

```cpp:CPPFunction.cpp
int32 ACPPFunction::Sum(int32 A, int32 B)
{
	A = 9;
	B = 7;
	return A + B;
}

int32 ACPPFunction::SumRef(int32& A, int32& B)
{
	A = 9;
	B = 7;
	return A + B;
}
```

値渡しのFunction[Sum]と、参照渡しのFunction[SumRef]を使用した後に、変数[CalcVarA],[CalcVarB]の値も確認できるように処理を編集します。

```cpp:CPPFunction.cpp BeginPlay()
case ECPPCalcType::Add:
{
	// Add(足し算)の処理
	// 値渡し
	int32 ResultAdd = Sum(CalcVarA, CalcVarB);
	FString StrResultAdd = FString::Printf(TEXT("Sum : %d + %d = %d"), CalcVarA, CalcVarB, ResultAdd);
	UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
	
	// 参照渡し
	ResultAdd = SumRef(CalcVarA, CalcVarB);
	StrResultAdd = FString::Printf(TEXT("SumRef : %d + %d = %d"), CalcVarA, CalcVarB, ResultAdd);
	UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
	break;
}
```

Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-13-31.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-17-33.png)

値渡しのFunction[Sum]と、参照渡しのFunction[SumRef]で出力結果が違います。
値渡しのFunction[Sum]の計算は「7 + 3 = 16」で間違っています。
参照渡しのFunction[SumRef]の計算は「9 + 7 = 16」で正しいです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-14-37-01.png)

値渡しのFunction[Sum]の計算は「7 + 3 = 16」で間違っています。

変数[CaclVarA]の値は[7]で、変数[CalcVarB]の値は[3]でした。
値渡しのFunction[Sum]内で、引数[A],[B]の値を変更しました。
しかし、変数[CaclVarA]、[CalcVarB]には影響がなかったので、計算結果が間違って出力されてしまいました。

値渡しでは、引数の型の領域が確保されて、値を引数に代入します。
変数[CalcVarA],[CalcVarB]は引数[A],[B]とは別の変数として扱われます。
なので、値渡しのFunction[Sum]内で引数[A],[B]の値を変更しても、変数[CalcVarA],[CalcVarB]の値は変わりませんでした。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-14-50-46.png)

参照渡しのFunction[SumRef]の計算は「9 + 7 = 16」で正しいです。

参照渡しのFunction[SumRef]内で引数[A],[B]に設定した値が、変数[CalcVarA],[CalcVarB]に設定されました。
引数[A],[B]の型に付けられた「&」は**「変数のアドレス」**です。
引数[A]に値を設定すると、引数[A]は変数[CalcVarA]のアドレスに値を設定します。
同じく引数[B]に値を設定すると、変数[CalcVarB]のアドレスに値を設定します。

参照渡しのFunction[SumRef]では、引数に設定した変数のアドレスに直接アクセスします。

値渡しはFunctionを呼び出した時に、領域を確保する分少し遅くなります。
参照渡しは変数に直接アクセスするので、領域を確保しないので値渡しより早くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-09-31.png)

### Blueprintで参照渡しをする

BlueprintでもInputを参照渡しにできます。
Inputに宣言した変数の左側[▽]をクリックすると、プロパティが表示されます。
[Pass-by-Reference]を有効にすると、ピンの形状が「ひし形」に変わり、参照渡しになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-16-48.png)


### 参照渡しの引数を関数内で変更させない（C++のみ）

**参照渡し**は軽くなる分、変数の値を変更されるリスクが伴います。
C++では引数の型の前に「const」を付けることで、関数内で引数を変更させないようにできます。

```cpp:CPPFunction.h
int32 SumRef(int32 &A, int32 &B);
    ↓
    ↓ 引数のVariableTypeの前にConstを付ける
    ↓
int32 SumRef(const int32 &A, const int32 &B);
```

constを付けた引数の値を変更してみましょう。

```cpp:CPPFunction.cpp
int32 ACPPFunction::SumRef(const int32& A, const int32& B)
{
	A = 9;
	B = 7;
	return A + B;
}
```

コンパイルすると、constを付けた変数に値を代入しようとした箇所がエラーになります。
constを付けることで安全に引数が使用されます。
Function内で引数の値を変更したくない場合は、constを付けると安全です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-25-17.png)

Blueprintでも変数に[Blueprint Read Only]を有効にすることで[const]を再現できました。
しかし、[Blueprint Read Only]を付けてしまうと、処理中に変数の値を変更できなくなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-27-12.png)


「値渡し」と「参照渡し」を確認できたので、処理を元に戻します。

```cpp:CPPFunction.cpp
int32 ACPPFunction::Sum(int32 A, int32 B)
{
	return A + B;
}

int32 ACPPFunction::SumRef(const int32& A, const int32& B)
{
	return A + B;
}
```

### 計算結果の文字列を取得するFunction[PrintCalcResult]を作成する

計算結果の文字列を取得するFunction[PrintCalcResult]をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-42-57.png)

「CPPFunction.h」にPrintCalcResultのプロトタイプを宣言します。
「Arg = Argument（引数）の略」です。

| Arg Index | Variable Type      | Arg Name      |
| --------- | ------------------ | ------------- |
| 0         | const ECPPCalcType | Type          |
| 1         | const int32        | A             |
| 2         | const int32        | B             |
| 3         | const float        | PrintDuration |

```cpp:CPPFunction.h
private:
    void PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration);
```

BlueprintにはInputにVariablesで宣言している名前を使用できました。
C++ではクラス内に同じ名前があるとエラーになるので、PrintDurationという重複しない名前を使用しています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-21-02-18.png)

BlueprintのFunction[PrintCalcResult]を確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-43-59.png)

C++でFunction[PrintCalcResult]を再現すると以下のようになります。

```cpp:CPPFunction.cpp PrintCalcResult()

void ACPPFunction::PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration)
{
	switch (Type)
	{
		case ECPPCalcType::Add:
		{
			// Add(足し算)の処理
			// 値渡し
			int32 ResultAdd = Sum(A, B);
			FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
			UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, PrintDuration);
			break;
		}
		case ECPPCalcType::Subtract:
		{
			// Subtract(引き算)の処理
			int32 ResultSubtract = A - B;
			FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
			UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, PrintDuration);
			break;
		}
		case ECPPCalcType::Multiply:
		{
			// Multiply(掛け算)の処理
			int32 ResultMultiply = A * B;
			FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
			UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, PrintDuration);
			break;
		}
		case ECPPCalcType::Divide:
		{
			// Divide(割り算)の処理(int > float)
			float ResultDivide = (float)A / (float)B;
			FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
			UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, PrintDuration);
		}
	}
}

```

次に、BlueprintのFunction[PrintCalcResult]を呼び出すBeginePlayを確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-49-02.png)

C++で再現すると以下のようになります。
こちらもソースコードがスッキリしました。

```cpp:CPPFunction.cpp BeginPlay()
void ACPPFunction::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	if (IsPrintHello)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		// 計算結果を出力する処理
		PrintCalcResult(CalcType, CalcVarA, CalcVarB, Duration);
	}
}
```

Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-13-31.png)

Level Editorの[Play]ボタンをクリックします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-09-17-33.png)

足し算の計算結果が出力されました。
Function[PrintCalcResult]が問題なく動作していることが確認できました。

Function化することで、何の処理をするのか明確になり読みやすくなります。

ソースコードが長くなった。読みづらくなった。

そのようなときにはFunction化を考えてみてはいかがでしょうか。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-15-56-36.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-16-00-41.png)

Visual StudioのSolutionもすべて保存しましょう。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## 参照URL

https://rinatz.github.io/cpp-book/ch04-03-scopes/


https://kinnaji.com/2020/01/28/passbyreference/


