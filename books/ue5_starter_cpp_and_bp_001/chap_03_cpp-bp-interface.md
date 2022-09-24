---
title: "【C++ & BP】インターフェース"
free: false
---

## インタフェース

### インタフェースについて

C++で作成したInterfaceをBlueprintで実装できるようにします。

### Blueprintで実装できるインタフェースを作成する

Blueprintで実装できるインタフェースを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-05-07.png)

親クラスに[UnrealInterface]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-06-19.png)

ClassTypeとClass名を設定します。

| Property   | Value          |
| ---------- | -------------- |
| Class Type | Public         |
| Name       | CPPBPInterface |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-08-49.png)

```cpp:CPPBPInterface.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "UObject/Interface.h"
#include "CPPBPInterface.generated.h"

// This class does not need to be modified.
UINTERFACE(MinimalAPI, Blueprintable)
class UCPPBPInterface : public UInterface
{
	GENERATED_BODY()
};

/**
 * 
 */
class CPP_BP_API ICPPBPInterface
{
	GENERATED_BODY()

	// Add interface functions to this class. This is the class that will be inherited to implement this interface.
public:

	// 引数と戻り値がないメンバ関数
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent, Category = "InterfaceTest")
	void PrintHello();

	// 引数と戻り値があるメンバ関数
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent, Category = "InterfaceTest")
	int Add(int A, int B);
};

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)


「BlueprintNativeEvent」はBlueprintとC++で実装できます。

```cpp
	// 引数と戻り値がないメンバ関数
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent, Category = "InterfaceTest")
	void PrintHello();

	// 引数と戻り値があるメンバ関数
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent, Category = "InterfaceTest")
	int Add(int A, int B);
```

「BlueprintImplementableEvent」はBlueprintだけが実装できます。

```cpp
	// 引数と戻り値がないメンバ関数
	UFUNCTION(BlueprintCallable, BlueprintImplementableEvent, Category = "InterfaceTest")
	void PrintHello();

	// 引数と戻り値があるメンバ関数
	UFUNCTION(BlueprintCallable, BlueprintImplementableEvent, Category = "InterfaceTest")
	int Add(int A, int B);
```

### インタフェースを実装するクラスを作成する

BlueprintInterfaceを設定するBlueprintを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-48-46.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-interface/2022-09-24-22-51-43.png)

名前を「BP_InterfaceTestCPP」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-24-23-52-42.png)

「Class Settings」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-24-23-53-55.png)

Interfaceに「CPPBPInterface」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-35-30.png)

Interfaceで追加した関数が「Interface」カテゴリに追加されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-37-24.png)

Outputを設定していない関数はEventとして実装できます。
関数を右クリック > [Implement event]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-38-45.png)

Implement eventを選択するとEvent Graphに関数名のイベントが追加されます。
追加されたEventに処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-39-50.png)

Outputを設定した関数は関数として処理を実装できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-40-58.png)

BeginPlayに動作確認する為の処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-43-35.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-44-23.png)

[BP_InterfaceTestCPP]をViewportにDrag&Dropします。
Vieportに[BP_InterfaceTest]があれば削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-46-13.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

インターフェースで実装したメンバ関数を呼び出せました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-interface/2022-09-25-00-46-58.png)

### 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/GameplayArchitecture/Interfaces/

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Types/Interface/UsingInterfaces/
