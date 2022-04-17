---
title: "Editor Utility Widget プリセットを保存する"
emoji: "👓"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5"]
published: true
---

## Editor Utility Widgetの入力値をSaveとLoadする

Editor Utility Widgetの入力値をSaveとLoadするEditorWidgetを作成します。

![](/images/articles/ue5-euw-save_preset/2022-04-10-17-23-09.png)

## Editor Utility Widgetを作成する

Editor Utility Widgetを作成します。
名前を「EUW_Preset」に設定します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-18-35-59.png)

Wighetを図のように配置します。

![](/images/articles/ue5-euw-save_preset/2022-04-10-17-36-01.png)

## Structure(構造体)を作成する

構造体を作成します。
名前を「FEUWData」に設定します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-18-33-57.png)

構造体に変数を追加します。

|Name |Type |
|---|---|
|Name |String |
|ValueString |String |
|ValueNumber |Integer |

![](/images/articles/ue5-euw-save_preset/2022-04-16-18-31-58.png)

## SaveGameの派生クラスを作成する

SaveGameの派生クラスを作成します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-18-50-14.png)

親クラスに「SaveGame」を選択します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-18-52-39.png)

名前を「BP_SaveGamePreset」に設定します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-18-57-41.png)

変数に「FEUWData」の型の変数を追加します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-19-18-40.png)

## Editor Utility Widgetの入力値を保存する

「EUW_Preset」に入力値を保存する処理を実装します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-19-03-18.png)

SaveボタンにOn Clickedイベントを追加します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-19-04-28.png)

BP_SaveGamePresetの変数を作成します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-19-21-33.png)

Widgetの入力値をBP_SaveGamePresetの変数SaveGameにセットします。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-06-50.png)

「Save Game to Slot」ノードで設定した値を保存します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-09-24.png)


## 保存した情報を読み込む

LoadボタンにOn Clickedイベントを追加します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-13-29.png)

保存したデータを読み込む処理を実装します。
保存するときと読み込むときはSlot Nameが一致するように設定します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-30-27.png)

読み込んだ情報をWidgetに設定します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-31-48.png)

CompileとSaveボタンをクリックします。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-33-34.png)

## 保存と読込を確認する

保存と読込の処理をEditorUtilityWidgetを実行して確認します。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-36-21.png)

TextBoxに値を入力してSaveボタンをクリックします。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-39-17.png)

入力値を消してからLoadボタンをクリックします。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-40-32.png)

保存した情報が読み込まれます。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-42-43.png)

保存した情報は「(プロジェクトフォルダ)/Saved/SaveGames」フォルダに(SlotName).savファイルとして保存されます。

![](/images/articles/ue5-euw-save_preset/2022-04-16-22-44-20.png)