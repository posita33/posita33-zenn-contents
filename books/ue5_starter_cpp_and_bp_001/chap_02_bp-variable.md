---
title: "【BP】Variable（変数）"
free: false
---

## 【Blueprint】Variable（変数）

### 今回できること

Variable（変数）を使用した処理に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-11-15-00-12.png)


複数のノードに同じ値を設定しようとした時に、ノードに直接入力すると、「入力の間違い」「入力の漏れ」といったヒューマンエラーが起きます。
変数を作成し、変数から値を取得するようにBlueprintを組んでおくことで、複数のノードで変数の値を使うことが約束されます。
また変数名を分かりやすい名前にしておくことで、可読性が上がります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-11-04.png)

### 学習用の新規レベル「Chapter_2_Variable」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-03-09-06-14-25.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Variable」を設定して、「Save」ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-32-14.png)

### Blueprintを複製する

学習でBlueprintを振り返れるように、ファイルが別々になるように複製します。
複製したいBlueprintを右クリックし、[Duplicate（複製）]を選択します。
ショートカットキーは[Ctrl + D]です。[Ctrl + C > Ctrl + V（コピー&ペースト）]でも同じことができますが、[Duplicate（複製）]は1回で複製できます。
名前を「BP_Variable」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-03-02-06-06-35.png)

### 変数を追加する（ノードのInputピンから）

「BP_Variable」をダブルクリックしてBlueprint Editorで開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-35-55.png)

Print Stringの[In String]を変数化します。
In StringのInputピンからDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-06-51.png)

メニューから「Promote to variable」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-07-06.png)

In Stringと書かれたノードが増えます。
InStringと書かれたノードとPrint StringのInputピンが接続されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-07-20.png)

### 変数の設定を変更する

My Blueprintパネルの「Variable」カテゴリーに「In String」という項目が増えています。これがVariable（変数）です。
Variable（変数）を選択すると[Detail]パネルに変数の設定が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-38-17.png)

[Detail]パネルの[Variable Name]を[Message]に変更します。
Print StringのIn Stringに接続していたノードの名称も「Message」に変換されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-40-23.png)

Default Value（初期値）を設定します。
しかし、Default Valueに「Please compile the blueprint」と表示されており、設定できません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-08-13.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-10-07-30-27.png)

Default Valueが設定できます。
InputピンからDrag&Dropして変数を作成すると、Inputピンに設定していた値がDefault Valueに設定されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-08-42.png)

再び、[Compile]ボタンをクリックして、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-45-10.png)

LevelEditorに戻り、Viewportに「BP_Variable」をDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-46-21.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

変数「Message」に設定されていたDefault Valueの文字列が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-47-30.png)

同じ結果です。
- Print StringのIn Stringに文字列を設定する。
- Print StringのIn Stringに変数の値を設定する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-01.png)

変数「Message」のDefault Valueを「BP Hello World!」変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-10-12.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-10-07-30-27.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

変数「Message」のDefault Valueを「BP Hello World!」が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-48-24.png)

複数のノードに同じ値を設定しようとした時に、ノードに直接入力すると、「入力の間違い」「入力の漏れ」といったヒューマンエラーが起きます。
変数を作成し、変数から値を取得するようにBlueprintを組んでおくことで、複数のノードで変数の値を使うことが約束されます。
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
DurationのVariableTypeは[Float]ということが分かりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-12-55-56.png)

[Variable Type]のリストから[Float]を選択します。
（Inputピンをマウスオーバーした時に表示されたVariable Type）

:::message
Unreal Engine Preview 1では[Float]が[Real]になりました。
Unreal Engine Preview 2で[Real]から[Float]に戻りました。
:::

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-12-58-31.png)

次にDefault Valueを設定します。
Default ValueはComplireしてから設定できるので、左上のComplireボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-00-56.png)

[Compile]することで、Default Valueが設定できます。
Print StringのDurationに設定された値[10.0]を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-02-19.png)

### 変数の値をGet（取得）する

変数「Message」ノードと同じように、Inputピンに接続するノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-04-03.png)

[Variavles]カテゴリーの[Duration]をDrag&Dropします。
マウスを離すと、メニューが表示されるので[Get Duration]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-05-13.png)

変数「Duration」の右側（Outputピン）からDrag&Dropし、[Print String]のDurationに接続します。
Variable Typeが一致しているので接続できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-39-18.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-10-07-30-27.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

文字列がDurationに設定した変数DurationのDefault Value[10.0]（10秒間）表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-06-28.png)

### 変数の値をSet（設定）する

次にPrint Stringで変数を使う前に、値を[3.0]（3.0秒）に変更するように変更します。
Get Durationを追加したのと同様に、変数[Duration]をEventGraphにDrag&Dropします。
マウスを離すとメニューが表示されるので、[Set Duration]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-07-47.png)

Setと書かれたノードの実行ピンを[Print String]が実行される前に実行されるように接続し直します。
Durationには[3.0]（3秒）を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-44-25.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-10-07-30-27.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

文字列がDurationに設定した変数DurationのDefault Value[10.0]（10秒間）ではなく、Setノードで設定した[3.0]（3秒）表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-09-31.png)

Default Valueは初期値なので、Setノードを使用すると処理の途中で値を変更できます。

### 変数をBlueprintReadOnlyに設定する（Default Valueから変更しない）

変数の値を途中で変えられてしまっては困る場合に、Setノードを使えなくし、Getノードのみしか使えなくできます。
[Blueprint Read Only]を有効にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-11-20.png)

Blueprint Edior左上の[Compile]ボタンをクリックすると、ノードの下部分に「Error！」と赤く表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-13-13.png)

Compiler Resultsにエラーメッセージが表示されます。
下線が付いている「Set Duraion」をクリックすると、エラーがあるノードにフォーカスがあいます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-11-14-35-10.png)

原因は[Blueprint Read Only]を有効にしたことで、変数[Duration]が読み取りだけになりました。変更しようとしたためErrorになりました。
Setノードは使えなくなったので削除します。Shift + Deleteキーで接続を維持したままノードを削除できます。
実行ピンを元に戻して、Blueprint Edior左上の[Compile]ボタンをクリックするとエラーが解消されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-16-04.png)

### Variable Type（変数の型）をCast（変数の型を別の型に変える）する

Variable Typeが一致していないと、変数とノードのInputピンを接続できません。しかし、Variable Typeが一致していなくても、Variable Typeを変更することで変数の値を設定できます。
DurationのDefault Value[10.0]を文字列として、[Print String]の[In String]で使用するように変更します。
変数[Duration]のOutputピンから[Print String]の[In String]にDrag&Dropします。
右下に「Convert Float to String」と表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-46-23.png)

Variable Typeを[Float]から[String]に変換するノードが中間に作成されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-46-35.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-10-07-30-27.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

DurationのDefault Valueである[10.0]が文字列として表示されます。
Variable Typeが一致していなくても、Variable Typeを変換できれば値を使用できます。
Blueprintでは変換できるVariable Typeであれば変換ノードを接続した時に作成してくれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-17-23.png)

### Variable Type（変数の型）のリストにないVariable Typeを検索して設定する

Variable Type（変数の型）のリストにないVariable Typeを設定について説明します。
今回はカラーを設定している[Print String]の[Text Color]ピンを変数化します。
まず、[Duration]ピンと同様に、[Text Color]ピンのVariable Typeを確認します。
マウスオーバーすると[Linear Color Structure]と表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-48-01.png)

変数[Duration]と同じように、[My Blueprint]タブから[+]ボタンをクリックして、変数を追加します。
変数を追加時にVariable Nameを変更できます。
Variable Nameは[TextColor]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-19-43.png)

DetailパネルからVariable Typeを設定します。
しかし、リストには[Linear Color Structure]というVariable Typeが表示されません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-22-25.png)

検索バーに[Linear Color]と入力します。
[Linear Color]と書かれた項目を選択します。
リストにない項目は検索することで見つけられます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-25-04.png)

次にDefault Valueを設定するので、Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-10-07-30-27.png)

LinearColorのDefault Valueは数値入力か[Color Picker]を使って色を設定できます。
Aと書かれたところを1.0に設定することを忘れないようにしてください。
AはAlpha（透明度）の数値なので、0.0が設定されていると、色を設定しても透明な文字として表示されます。1.0に設定して不透明な文字に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-49-25.png)

変数の設定ができたので、変数[TextColor]のGetノードをEventGraphに追加します。
変数を[Ctrl]キーを押しながらDrag&Dropするとメニューが表示されずにGetノードが追加されます。
Setノードは[Alt]キーを押しながらDrag&Dropすると追加できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-30-48.png)

変数[TextColor]のGetノードと[Print String]の[Text Color]ピーンを接続します
文字列の出力を変数[Message]に戻し、変換ノードを削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-50-13.png)

Blueprint Edior左上の[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-32-06.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

表示される文字列の色が変数[TextColor]に設定した色で表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-32-39.png)

### 変数のCategoryを設定する

変数は作成していくにつれて増えていき、やがて何に使っているのか分からなくなります。
そんな時に便利なのが[Category]設定です。
[Category]は変数をグループ化できます。
[Print String]で使用している変数を[Print String]Categoryに設定します。

上から順番にCategoryを設定します。
Categoryはリストに[Default]しかないので、最初は入力してCategoryを増やします。
Categoryに[Print String]を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-35-35.png)

Variavlesカテゴリーに[Print String]というCategoryが作成され、変数[Message]がメンバーとして登録されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-37-34.png)

Categoryへのメンバー登録は2パターンあります。
- 変数をCategoryにDrag&Drop
- 変数のCategoryからリスト選択

変数[Duration]を[Print String]CategoryにDrag&Dropします。
変数[Duration]が[Print String]Categoryのメンバーになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-40-13.png)

変数[TextColor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-41-34.png)

Categoryのリストから[Print String]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-42-32.png)

Print Stringで使用している変数が[Print String]Categoryのメンバーになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-44-58.png)

Categoryを整理することでVariavlesカテゴリーが見やすくなります。

- 何で使われている変数かわかる
- 折りたためるので、関係のない変数を非表示にできる

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-01-27-07-52-35.png)

### すべて保存する

他にも変数の設定項目がありますが、Blueprint用のクラスや変数をC++で作成する時に説明します。

コンテンツブラウザの[Save All]をクリックし、保存されていないアセットを保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-13-46-12.png)

## 【参照URL】

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/Variables/
