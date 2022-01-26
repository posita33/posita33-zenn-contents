---
title: "【BP】 Variable(変数)"
emoji: "😽"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---


## 【Blueprint】Variable（変数）

### 今回できること

**【要追記！ 】**


## 学習用の新規レベル「Chapter_2_Variable」を作成する

学習用に新規レベルを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-05-26.png)

[Empty Level]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-05-41.png)

作成したレベルを保存します（File > Save Current Level）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-05-54.png)

名前を「Chapter_2_4_Variable」に設定して、「Save」ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-06-15.png)

### 変数を追加する（ノードのInputピンから）
「BP_SampleActor」をダブルクリックしてBlueprint Editorで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-06-37.png)

Print Stringの[In String]を変数化します。
In StringのInputピンからDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-06-51.png)

メニューから「Promote to variable」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-07-06.png)

In Stringと書かれたノードが増えます。
InStringと書かれたノードとPrint StringのInputピンが接続されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-07-20.png)

### 変数の設定を変更する

My Blueprintパネルの「Variable」カテゴリーに「In String」という項目が増えています。これが変数（Variable）です。
変数を選択するとDetailパネルに変数の設定が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-07-39.png)

Detailパネルの[Variable Name]を[Message]に変更します。
Print StringのIn Stringに接続していたノードの名称も「Message」に変換されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-07-56.png)

Default値（初期値）を設定します。
しかし、Default Valueに「Please compile the blueprint」と表示されており、設定できません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-08-13.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-08-29.png)

Default Valueが設定できます。
InputピンからDrag&Dropして変数を作成すると、Inputピンに設定していた値がDefault Valueに設定されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-08-42.png)

再び、[Compile]ボタンをクリックして、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-08-55.png)

LevelEditorに戻り、Viewportに「BP_SampleActor」をDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-09-08.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-09-19.png)

変数「Message」に設定されていたDefault Valueの文字列が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-09-31.png)

同じ結果です。
- Print StringのIn Stringに文字列を設定する。
- Print StringのIn Stringに変数の値を設定する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-01.png)

変数「Message」のDefault Valueを「BP Hello World!」変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-12.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-26.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-41.png)

変数「Message」のDefault Valueを「BP Hello World!」が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-52.png)

複数のノードに同じ値を設定しようとした時に、ノードに直接入力すると、「入力の間違い」「入力の漏れ」といったヒューマンエラーが起きます。
変数を作成し、変数から値を取得するようにBlueprintを組んでおくことで、複数のノードで変数の値を使わことが約束されます。
また変数名を分かりやすい名前にしておくことで、可読性が上がります。
処理の流れを追いやすくなります。
変数の名前は非常に大事なのですごく悩みます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-11-04.png)


### 変数を追加する（My BlueprintパネルのVariableカテゴリーから）

Print StringのDurationピンに変数を追加して設定します。
変数はMy BlueprintパネルのVariablesカテゴリーから追加できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-12-18.png)

[Variables]カテゴリーの右側[＋]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-12-28.png)

[Variables]カテゴリーに変数が追加されます。
変数の設定をDetailパネルで設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-12-53.png)

[Variable Name（変数名）]を[Duration]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-13-45.png)


次に[Variable Type（変数の型）]を設定します。
設定したいInputピンにマウスオーバーします。
表示される文字（ToolTip）からInputピンのVariableTypeを確認します。
DurationのVariableTypeはFloatということが分かりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-13-55.png)


[Variable Type]のリストから[Float]を選択します。
（Inputピンをマウスオーバーした時に表示されたVariable Type）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-38-26.png)

次にDefault Valueを設定します。
Default ValueはComplireしてから設定できるので、左上のComplireボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-36-52.png)

[Compile]することで、Default Valueが設定できます。
Print StringのDurationに設定された値[10.0]を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-37-05.png)

### 変数の値をGet（取得）する

変数「Message」ノードと同じように、Inputピンに接続するノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-38-53.png)

[Variavles]カテゴリーの[Duration]をDrag&Dropします。
マウスを離すと、メニューが表示されるので[Get Duration]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-39-03.png)

変数「Duration」の右側（Outputピン）からDrag&Dropし、[Print String]のDurationに接続します。
Variable Typeが一致しているので接続できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-39-18.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-39-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-39-45.png)

文字列がDurationに設定した変数DurationのDefault Value[10.0](10秒間)表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-39-58.png)

### 変数の値をSet（設定）する
次にPrint Stringで変数を使う前に、値を[3.0](3秒)に変更するように変更します。
Get Durationを追加したのと同様に、変数[Duration]をEventGraphにDrag&Dropします。
マウスを離すとメニューが表示されるので、[Set Duration]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-42-51.png)

Setと書かれたノードの実行ピンを[Print String]が実行される前に実行されるように接続し直します。
Durationには[3.0]（3秒）を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-44-25.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-44-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-44-41.png)

文字列がDurationに設定した変数DurationのDefault Value[10.0](10秒間)ではなく、Setノードで設定した[3.0](3秒)表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-44-51.png)

Default Valueは初期値なので、Setノードを使用すると処理の途中で値を変更できます。

### 変数をBlueprintReadOnlyに設定する（Default Valueから変更しない）

変数の値を途中で変えられてしまっては困る場合に、Setノードを使えなくし、Getノードのみしか使えなくできます。
[Blueprint Read Only]を有効にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-45-20.png)

Blueprint Edior左上の[Compile]ボタンをクリックすると、ノードの下部分に「Error！」と赤く表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-45-32.png)

Compiler Resultsにエラーメッセージが表示されます。
下線が付いている「Set Duraion」をクリックすると、エラーがあるノードにフォーカスがあいます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-45-44.png)

原因は[Blueprint Read Only]を有効にしたことで、変数[Duration]が読み取りだけになりました。変更しようとしたためErrorになりました。
Setノードは使えなくなったので、削除します。
実行ピンを元に戻して、Blueprint Edior左上の[Compile]ボタンをクリックするとエラーが解消されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-46-01.png)

### Variable Type（変数の型）をCast（変数の型を別の型に変える）する
Variable Typeが一致していないと、変数とノードのInputピンを接続できません。しかし、Variable Typeが一致していなくても、Variable Typeを変更することで変数の値を設定できます。
DurationのDefault Value[10.0]を文字列として、[Print String]の[In String]で使用するように変更します。
変数[Duration]のOutputピンから[Print String]の[In String]にDrag&Dropします。
右下に「Convert Float to String」と表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-46-23.png)

Variable Typeを[Float]から[String]に変換するノードが中間に作成されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-46-35.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-46-52.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-47-05.png)

DurationのDefault Valueである[10.0]が文字列として表示されます。
Variable Typeが一致していなくても、Variable Typeを変換できれば値を使用できます。
Blueprintでは変換できるVariable Typeであれば変換ノードを接続した時に作成してくれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-47-19.png)

### Variable Type（変数の型）のリストにないVariable Typeを検索して設定する

Variable Type（変数の型）のリストにないVariable Typeを設定について説明します。
今回はカラーを設定している[Print String]の[Text Color]ピンを変数化します。
まず、[Duration]ピンと同様に、[Text Color]ピンのVariable Typeを確認します。
マウスオーバーすると[Linear Color Structure]と表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-48-01.png)

変数[Duration]と同じように、[My Blueprint]タブから[+]ボタンをクリックして、変数を追加します。
変数を追加時にVariable Nameを変更できます。
Variable Nameは[TextColor]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-48-13.png)

DetailパネルからVariable Typeを設定します。
しかし、リストには[Linear Color Structure]というVariable Typeが表示されません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-48-39.png)

検索バーに[Linear Color]と入力します。
[Linear Color]と書かれた項目を選択します。
リストにない項目は検索することで見つけられます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-48-49.png)

次にDefault Valueを設定するので、Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-49-05.png)

LinearColorのDefault Valueは数値入力か[Color Picker]を使って色を設定できます。
Aと書かれたところを1.0に設定することを忘れないようにしてください。
AはAlpha（透明度）の数値なので、0.0が設定されていると、色を設定しても透明な文字として表示されます。1.0に設定して不透明な文字に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-49-25.png)

変数の設定ができたので、変数[TextColor]のGetノードをEventGraphに追加します。
変数を[Ctrl]キーを押しながらDrag&Dropするとメニューが表示されずにGetノードが追加されます。
Setノードは[Alt]キーを押しながらDrag&Dropすると追加できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-49-49.png)

変数[TextColor]のGetノードと[Print String]の[Text Color]ピーンを接続します
文字列の出力を変数[Message]に戻し、変換ノードを削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-50-13.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-50-24.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-50-36.png)

表示される文字列の色が変数[TextColor]で設定した。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-50-47.png)

### 変数のCategoryを設定する

変数は作成していくにつれて増えていき、やがて何に使っているのか分からなくなります。
そんな時に便利なのが[Category]設定です。
[Category]は変数をグループ化できます。
[Print String]で使用している変数を[Print String]Categoryに設定します。

上から順番にCategoryを設定します。
Categoryはリストに[Default]しかないので、最初は入力してCategoryを増やします。
Categoryに[Print String]を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-54-45.png)

Variavlesカテゴリーに[Print String]というCategoryが作成され、変数[Message]がメンバーとして登録されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-55-27.png)

Categoryへのメンバー登録は2パターンあります。
- 変数をCategoryにDrag&Drop
- 変数のCategoryからリスト選択

変数[Duration]を[Print String]CategoryにDrag&Dropします。
変数[Duration]が[Print String]Categoryのメンバーになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-51-28.png)

変数[TextColor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-51-45.png)

Categoryのリストから[Print String]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-51-55.png)

Print Stringで使用している変数が[Print String]Categoryのメンバーになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-52-07.png)

Categoryを整理することでVariavlesカテゴリーが見やすくなります。

- 何で使われている変数かわかる
- 折りたためるので、関係のない変数を非表示にできる

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-52-35.png)


### すべて保存する

他にも変数の設定項目がありますが、Blueprint用のクラスや変数をC++で作成する時に説明します。

コンテンツブラウザの[Save All]をクリックし、保存されていないアセットを保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-53-05.png)

## 【参照URL】

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Variables/
