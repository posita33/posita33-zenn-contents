---
title: "Editor Utility Widgetのプリセット情報をリスト化する"
emoji: "💼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5"]
published: true
---

## Presetをリスト化して保存、読込できるようにする

Preset名でプリセットを保存して、リストからプリセット名を選択して読み込めるようにします。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-22-12.png)

## SaveGameの派生クラスにプリセット名を格納するString配列を追加する

SaveGameの派生クラスである「BP_SaveGamePreset」にプリセット名を格納するString配列の変数を追加します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-09-56-24.png)

|Name |Type |
|---|---|
|NameArray|String(配列)|

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-09-56-53.png)

## Widgetを追加する

Preset名を入力するTextBoxと、Preset名を選択するComboBoxを追加します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-00-47.png)

Widgetを図のように追加します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-09-46-33.png)

## Preset名を保存できるようにする

Saveボタンの「On Clicked」イベントに処理を追加します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-06-53.png)

変数を追加します。

|Name |Type |
|---|---|
|LocalSaveName|BP_SaveGamePreset|
|NameArrayLocal |String(配列) |

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-35-07.png)

プリセット名を保存するSaveGameファイルを作成します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-31-36.png)

プリセット名を「SaveNames」という名前で保存します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-32-17.png)

「SaveNames」を読み込みます。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-32-45.png)

「SaveNames」に保存されたプリセット名をComboBoxに追加します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-33-13.png)

プリセット名に設定した名前のSaveGameにWidgetの入力値を保存します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-18-50.png)

## Preset名で読み込めるようにする

Loadボタンの「On Clicked」イベントに処理を追加します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-10-41-15.png)

Preset名のSaveGameがある場合にWidgetの入力値を更新します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-04-26.png)

## EditorUtilityWidgetを立ち上げた時にPresetのリストを更新する

ウィジェットを立ち上げた時に「SaveNames」のSaveGameが存在すればConboBoxのリストを更新します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-09-56.png)

## 保存と読込を確認する

実装した処理を確認します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-14-01.png)

Widgetに入力した値にプリセット名を付けてSaveボタンをクリックします。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-16-58.png)

リストにプリセット名が追加されているので選択します。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-16-14.png)

プリセット名を選択した状態で「Load」ボタンをクリックすると入力値がWidgetに設定されます。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-20-39.png)

保存した情報は「(プロジェクトフォルダ)/Saved/SaveGames」フォルダにSaveNames.savと(Preset).savファイルが保存されます。

![](/images/articles/ue5-euw-save_preset_list/2022-04-17-11-37-10.png)


## サンプルプロジェクト(GitHub)

GitHubにサンプルプロジェクトを置いておきました。

https://github.com/posita33/EUWPreset