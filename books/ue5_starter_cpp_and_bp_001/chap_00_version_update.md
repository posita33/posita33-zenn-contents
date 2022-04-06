---
title: "バージョンアップによる変更点"
free: false
---

## バージョンアップについて

Unreal Engineは年間で2~3バージョンがアップします。
バージョンアップではUIが変わり手順の画像とは違う文字になったり、アイコンの場所が変わります。
本の画像がバージョンアップに追いついていないことがあります。
このページでは本に影響があるバージョンアップによる変更点をまとめています。

## UE5 5.0.0(2022/4/6)

UE5の正式版が使用できるようになりました。
リリースノートが公開されているので一読しましょう。

https://docs.unrealengine.com/5.0/ja/unreal-engine-5-0-release-notes/

## UE5 Preivew 2

2022/2/23にUE5 Preview 2が使用できるようになりました。
Preview1から変更点があるので、正式版まで変更がありそうです。

BasicレベルのFloorの形状やMaterialが変更されました。
レベルの選択画面の並び順が変わりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-09-06-03-22.png)

Preview1で[Real]型になりましたが、Preview2で[Float]型に戻りました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-09-06-11-20.png)

## UE5 Preivew 1

2022/2/23にUE5 Preview 1が使用できるようになりました。
UE5の正式版に近づきました。

Editorのメニュー、ツールバーに変更がありました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-09-25-26.png)

Contents Browserのフォルダが[All]フォルダから開始するようになりました。
選択した時の色が濃い青になりました。
アイコンが変わっています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-09-31-47.png)

複製（Duplicate）のショートカットが「Ctrl + D」に変更されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-10-35-55.png)

BlueprintのFloat型の表示がReal型に変わりました。
これはFloat型に戻るのではないかと思いますが、Real型で学習できるように画像を編集します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-09-36-35.png)

PrintStringノードのInputピンに[Key]が追加されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-09-40-20.png)

[Key]を設定しておくと、同じ[Key]のPrintStringは1つしか出力されなくなります。
[Key]を設定したPrintStringが表示されている間に同じ[Key]の設定をしたPrintStringが呼ばれると、メッセージが上書きされます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-09-41-22.png)

UE5 Preview 1ではLiveCodingが有効になっているので、Editorを開いている状態でBuildすると、UnrealBuildToolsがエラーになります。
Editorを開いている状態では、[Ctrl + Alt + F11]を押すことでEditor上のコンパイルを実行できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-35-35.png)

UE5のLevelEditor右下の小さいアイコンがC++のソースコードをコンパイルするボタンなので、アイコンをクリックするとコンパイルが実行されます。
「Live coding succeeded」が表示されればコンパイル成功です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

列挙型(Enumeration)エディタのUIが変わりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-05-16-24-36.png)

構造体(Structure)エディタのUIが変わりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-06-00-20.png)

UE5 Preview 1から変数の設定、Default Valueの設定でタブが分かれました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_00_version_update/2022-03-06-19-23-24.png)

