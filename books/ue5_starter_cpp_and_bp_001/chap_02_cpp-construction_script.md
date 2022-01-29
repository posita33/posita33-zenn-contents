---
title: "【C++】Construction Script"
free: false
---

## 【C++】Construction Script

### C++でBlueprintを再現すること

C++でBlueprintのConstruction Scriptで実装した処理を再現します。

- 宣言した変数がLevelEditorの[Detail]パネルで変更できる
- PointLightの表示/非表示（Set Visibilityノード）
- PointLightの光の強さ調整（Set Intensityノード）
- PointLightの光の色調整（Set LightColorノード）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-57-24.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-57-36.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-57-43.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-57-53.png)

### Visual Studioを開いて、編集するファイルを表示する

プロジェクトを閉じていたら、プロジェクトを開き、
「Chapter_2_6_ConstructionScript」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-48-29.png)

ToolsからVisual Studioを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-49-19.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPSampleActor.cpp
- CPPSampleActor.h

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-49-36.png)



### LevelEditorで編集可能な変数を追加する
「CPPSampleActor.hのpublic」に変数を追加します。

```cpp:CPPSampleActor.h
public:
	UPROPERTY(EditAnywhere, Category = "Point Light")
	bool bIsVisible = false;

	UPROPERTY(EditAnywhere, Category = "Point Light")
	float Intensity = 5000.0f;

	UPROPERTY(EditAnywhere, Category = "Point Light")
	FLinearColor LightColor = FLinearColor::White;
```

UPROPERTY識別子で編集可能（EditAnyWhere）、Categoryを[Point Light]に設定しています。

```cpp
UPROPERTY(EditAnywhere, Category = "Point Light")
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-13-59-59.png)

LevelEditorのViewportに「CPPSampleActor」をDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-00-17.png)

「CPPSampleActor」の[Detail]パネルをスクロールすると、[Point Light]Catetoryがあります。
「CPPSampleActor.hのpublic」に追加した変数が表示されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-00-31.png)

OnConstruction関数でPointLightの表示/表示を設定する
次にBlueprintのConstructionScriptタブを再現します。
C++では[OnConstruction]をオーバーライドします。
親クラスである[AActor]で定義されている関数を子である[ACPPSampleActor]で関数を上書きします。OverrideについてはClassの継承で詳しく説明します。

```cpp:CPPSampleActor.h
protected:
	virtual void OnConstruction(const FTransform& Transform) override;
```

OnConstructionではPointLightのSetVisibility関数に変数[bIsVisible]を引数に渡して呼び出します。

```cpp:CPPSampleActor.cpp
void ACPPSampleActor::OnConstruction(const FTransform& Transform)
{
	// PointLightの表示・非表示を設定
	PointLight->SetVisibility(bIsVisible);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-02-02.png)

LevelEditorの[Detail]パネルで変数[IsVisible]を有効/無効に切り替えます。
変数[bIsVisible]が有効になるとPointLightが表示され、無効になるとPointLightが非表示になります。

bを先頭に付けた変数はプロパティには、先頭の"b"が表示されません。先頭の"b"はbooleanの変数であるということを明記させるために付け、UnrealEngine のEditorでは表示されません（少し特殊な名前の扱いです）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-02-15.png)

### OnConstruction関数でPointLightのIntesity（光の強さ）を調整をする

次に、PointLightのIntensity（光の強さ）を調整します。
PointLightのSetIntensity関数に変数[Intensity]を引数に渡して呼び出します。

```cpp:CPPSampleActor.cpp
void ACPPSampleActor::OnConstruction(const FTransform& Transform)
{
	// PointLightの表示・非表示を設定
	PointLight->SetVisibility(bIsVisible);

	// PointLightの強さを設定
	PointLight->SetIntensity(Intensity);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-03-02.png)

LevelEditorの[Detail]パネルで変数[Intensity]の値を大きくすると光が強くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-03-13.png)

OnConstruction関数でPointLightのLightColor（光の色）を調整をする
最後に、PointLightのLightColorを変更します。
PointLightのSetLightColor関数に変数[LightColor]を引数に渡して呼び出します。

```cpp:CPPSampleActor.cpp
void ACPPSampleActor::OnConstruction(const FTransform& Transform)
{
	// PointLightの表示・非表示を設定
	PointLight->SetVisibility(bIsVisible);

	// PointLightの強さを設定
	PointLight->SetIntensity(Intensity);

	// PointLightのLightColorを設定
	PointLight->SetLightColor(LightColor);
}
```
Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-03-47.png)

LevelEditorの[Detail]パネルで変数[LightColor]をクリックすると、ColorPickerが表示されます。色を選択して、OKボタンをクリックすると光の色が選択した色に変わります。
BlueprintのConstructionScriptをC++側ではOnConstruction関数で再現できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-04-00.png)

https://zenn.dev/posita33/articles/41737b3be89aa4

### C++OnConstruction関数とBlueprintのConstructionScript

変数はUPROERTYでEditAnyWhereを設定することで、Blueprint側のInstance Editableを有効にした時と同様に扱えました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-04-34.png)

BlueprintのConstructionScriptをC++側ではOnConstruction関数で再現できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-04-44.png)

Blueprintで使用しているノード名とC++で使用している関数名は同じということに気付きます。
PointLightの表示/非表示はPointLightComponentの[SetVisibility]関数から設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-05-09.png)

PointLightの光の強さはPointLightComponentの[SetIntensity]関数から設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-05-20.png)

PointLightの光の色はPointLightComponentの[SetLightColor]関数から設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-05-35.png)

### すべて保存する

C++側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-construction_script/2022-01-27-14-06-00.png)

### 最終的なソースコード

```cpp:CPPSampleActor.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Components/ArrowComponent.h" // 追加
#include "Components/PointLightComponent.h" // 追加
#include "CPPSampleActor.generated.h"

UCLASS()
class CPP_BP_API ACPPSampleActor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPSampleActor();

	// Scene Component
	UPROPERTY(EditAnywhere)
		USceneComponent* DefaultSceneRoot;

	// StaticMesh Component
	UPROPERTY(EditAnywhere)
	UStaticMeshComponent* StaticMesh;

	// Arrow Component
	UPROPERTY(VisibleAnywhere)
	UArrowComponent* Arrow;

	// PointLightComponent Component
	UPROPERTY(EditAnywhere)
	UPointLightComponent* PointLight;

	UPROPERTY(EditAnywhere, Category = "Point Light")
	bool bIsVisible = false;

	UPROPERTY(EditAnywhere, Category = "Point Light")
	float Intensity = 5000.0f;

	UPROPERTY(EditAnywhere, Category = "Point Light")
	FLinearColor LightColor = FLinearColor::White;

	// DurationのGet関数
	float GetDuration() { return Duration; }

	// TextColorのGet関数
	FLinearColor GetTextColor() { return TextColor; }

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

	virtual void OnConstruction(const FTransform& Transform) override;

public:
	// Called every frame
	virtual void Tick(float DeltaTime) override;

private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FColor(255, 255, 255);
};
```

```cpp:CPPSampleActor.cpp OnConstruction()
void ACPPSampleActor::OnConstruction(const FTransform& Transform)
{
	// PointLightの表示・非表示を設定
	PointLight->SetVisibility(bIsVisible);

	// PointLightの強さを設定
	PointLight->SetIntensity(Intensity);

	// PointLightのLightColorを設定
	PointLight->SetLightColor(LightColor);
}
```

## 【参照URL】

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/ActorLifecycle/

https://qiita.com/bigengelt/items/b17545fffe7b8d69e5e8

イスラエルの方のUnrealEngine C++まとめページです。
UE4のC++でできることがまとまっているので、参考になります。
https://jip.dev/notes/unreal-engine/
