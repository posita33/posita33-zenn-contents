---
title: "WebカメラからAIがモーションを作ってくれるPlask モーションデータをUE5で使用する"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue4", "ue5"]
published: true
---

## VideoからAIが解析してMotionデータを作成してくれるサービス「Plask」
VideoからAIが解析してMotionデータを作成してくれるサービス「Plask」

https://80.lv/articles/plask-a-new-free-tool-for-extracting-3d-motion-from-videos/

Plaskで作成したモーションデータをUE5のMannequinで使えるようにします。

https://twitter.com/posita33/status/1483746174599598083

### ProjectをGitHubに公開しました。
UE5のProjectをGitHubに公開しました。
よかったら使ってください。
https://github.com/posita33/PlaskToUE5


### Plaskにサインアップする
Plaskは無料で使用できます。
Plaskを使用するためにSignUpします。

https://plask.ai/

![](/images/articles/plask-to-unrealengine/2022-01-19-19-44-19.png)

Googleアカウントかメールアドレスでサインアップできます。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-45-15.png)

この後にアカウント名を決めるウィンドウで、アカウント名を設定します。

### PlaskでWebカメラからモーション動画を撮影する

トップページの[Get Started]をクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-46-15.png)

右上の[カメラアイコンを]クリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-49-52.png)

灰色になっている箇所にWebカメラの映像が写ります。
Webカメラの選択は、右上の[Camera]から選択します。
Webカメラの設定できたら、「録画ボタン(赤丸)」をクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-53-18.png)

録画を終了するには再び「録画ボタン(赤丸)」をクリックします。
録画が完了するとプレビューが表示されるます。
一番下のタイムラインでアニメーションにしたい範囲を指定します。
範囲が指定できたら、「Extract Motion」をクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-57-07.png)

Motionの抽出が始まります。大体の完了時間が表示されます。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-58-49.png)

Motionの抽出が終わると、Motion名を設定するダイアログが表示されます。
Motion名を設定して、[OK]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-19-58-22.png)


### Plaskでスマホ動画からモーションデータを抽出する
:::message
動画からモーションデータを抽出方法が分かりました。(2022/1/22)
動画からモーションデータを抽出したい方はコチラをご参照ください。
:::

:::message alert
使用する動画は横長の動画をお使いください。
幅の長い方を【横】として扱われるので、縦長動画は左のお腹が上になってしまいます。
:::

![](/images/articles/plask-to-unrealengine/2022-01-22-11-00-00.png)  

:::details 動画からモーションデータを抽出する手順

動画からのモーションデータ抽出はPlask公式チャンネルの動画を参考にしました。
ありがとうございます！
https://www.youtube.com/watch?v=pzpbS5G71MU

[Library]の[+]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-29-01.png)

モーションを抽出する動画を選択します。
幅の長い方を横と判断するので、横長動画を選択してください。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-33-48.png)

抽出を確認するダイアログが表示されるので、[Confirm]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-40-32.png)

Webカメラの時と同様です。
抽出する範囲を選択し、[Extract Motion]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-43-45.png)

Motion名を設定して、[OK]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-45-11.png)

抽出にかかる時間が表示されます。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-45-40.png)

Libraryパネルに設定したMotion名が追加されました。
![](/images/articles/plask-to-unrealengine/2022-01-22-10-47-04.png)
:::

### PlaskのMannequinに撮影したアニメーションを反映する
Motionの抽出すると最初の画面に移動します。
左側の「Library」から「Mannequin_glb」をViewportにDrag&Dropします。
![](/images/articles/plask-to-unrealengine/2022-01-19-20-53-19.png)

さきほど設定したMotion名を「Mannequin_glb」にDrag&Dropします。
![](/images/articles/plask-to-unrealengine/2022-01-19-20-51-03.png)

「Mannequin_glb」に入った「Motion名」をViewportの真ん中のMannequinにDrag&Dropします。
![](/images/articles/plask-to-unrealengine/2022-01-19-20-51-56.png)

タイムラインの再生ボタンをクリックすると、Motionが再生されます。
![](/images/articles/plask-to-unrealengine/2022-01-19-20-57-19.png)


### PlaskのモーションデータをFBXにExportする

「Mannequin_glb」内のMotion名を右クリック > Export
![](/images/articles/plask-to-unrealengine/2022-01-19-21-00-11.png)

表の設定をして、[Export]ボタンをクリックします。
| Property | Value    |
| -------- | -------- |
| Motion   | bindPose |
| Format   | FBX      |

![](/images/articles/plask-to-unrealengine/2022-01-19-21-01-20.png)

Exportまでかかる時間が表示されます。

![](/images/articles/plask-to-unrealengine/2022-01-19-21-01-45.png)

Exportが完了するとFBXがダウンロードされます。
名前を「SK_PlaskMannequin.fbx」に設定します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-04-02.png)

次に、Motion名を設定したMotionをExportします。
「Mannequin_glb」内のMotion名を右クリック > Export
![](/images/articles/plask-to-unrealengine/2022-01-19-21-05-15.png)

表の設定をして、[Export]ボタンをクリックします。
| Property | Value                    |
| -------- | ------------------------ |
| Motion   | （設定したモーション名） |
| Format   | FBX                      |

![](/images/articles/plask-to-unrealengine/2022-01-19-21-06-10.png)

名前を「SK_PlaskMannequin_(Motion名).fbx」に設定します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-10-03.png)


### Plaskのマニュアル
他にもPlask上でできることがあるので、時間を見つけて試してみます。
https://plasticmask.notion.site/User-guide-ac4bba1b75384c309e7a24e6542454ba

YouTubeチャンネルにチュートリアル動画が上がっています。
https://www.youtube.com/channel/UClHOCrckvQEcrkqH4A7PA5A


## UE5でMannequinにPlaskのMotionをImportする
UE5にPlaskからExportしたMotionをImportします

### UE5のProjectを作成する

UE5 EAでプロジェクトを作成します。
「SK_Mannequin」を使用するので、「ThirdPerson」テンプレートを選択します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-12-55.png)!

プロジェクトが作成されたら「Plask」のMotionインポート用のフォルダを作成します
![](/images/articles/plask-to-unrealengine/2022-01-19-21-17-55.png)


### BasePoseとなるFBX「SK_PlaskMannequin.fbx」をImportする
まずは、BasePoseとなるFBX「SK_PlaskMannequin.fbx」をImportします。
作成した「Meshes」フォルダにImportします。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-20-39.png)

設定を変えずに[Import]ボタンをクリックします
![](/images/articles/plask-to-unrealengine/2022-01-19-21-27-40.png)

BasePoseとなるMeshとSkeltonがImportされました。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-29-04.png)

### Plaskで作成したMotionをImportする

Plaskで作成したMotion「SK_PlaskMannequin_(Motion名).fbx」を「Animations」フォルダにImportします。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-30-35.png)

[Import Mesh]のチェックを外します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-32-02.png)

[Skelton]に「SK_PlaskMannequin_Skelton」を設定します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-33-01.png)

[Import Rotation]のXに[90.0]を設定します。
設定を忘れても、あとで直し方を解説します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-34-11.png)

MotionがImportされました。
ダブルクリックして開くと、Plaskで作成したMotionが再生されます。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-36-00.png)

### Import RotaionのX:0.0でImportした場合

FBX Importの際に[Import Rotation]の設定を行わない場合の対処法です。

![](/images/articles/plask-to-unrealengine/2022-01-19-21-37-25.png)

ImportするとMotionのMannequinが寝っ転がった状態でアニメーションします。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-40-16.png)

左側の設定から、[Import Rotation]のXに[90.0]を設定します。
[Reimport Animation]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-43-02.png)

MotionのMannequinが立った状態で再生されるようになります。
[Save]ボタンをクリックします。

UnityのYUpのモデルやMotionをインポートした対処法が役に立ちました。
PlaskはUEのMannequinが使われていますが、中身はUnityで使用されるように作られています。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-44-34.png)

### すべて保存する
ここで一度すべて保存しましょう。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-45-47.png)


## UE5でMannequinにPlaskのAnimationをリターゲットする
Plaskで作成したMotionやBasePoseのFBXがImportできたので、PlaskのMotionをUE5のMannequinで動くようにしましょう。

### PlaskのMannequinはMixamoに似ている
UnrealEngineのSK_MannequinとPlaskのMannequinのSkeltonのTree構造を比較しました。
Plask側はUnityの「Unity Humanoid Avatar」ですぐに動きそうな構造をしています。
https://virtualcast.jp/wiki/unity/humanoid/introduction

**MixamoのアニメーションをUnrealEngineで動かす方法**が一番近いと判断しました。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-50-41.png)


「**MixamoからUE5(UE4)へアニメーションをリターゲットして使用する方法**」を参考にさせていただきました。
ありがとうございます！

https://zenn.dev/daichi_gamedev/books/unreal-engine-5/viewer/mixamo-to-ue

「**UnrealEngine5の教科書**」素晴らしいです。
現在ZennでBookを作成する際に、参考にさせていただいてます。
https://zenn.dev/daichi_gamedev/books/unreal-engine-5

## SK_PlaskMannequinのRigをSetUpする
リターゲットできるように、異なるSkelton通しを対応させる設定を行います。

「SK_PlaskMannequin」を開いて、「Retarget Manager」を開きます。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-55-43.png)

[Set up Rig]カテゴリーの[Slect Rig]に[Humanoid Rig]を設定します。
![](/images/articles/plask-to-unrealengine/2022-01-19-21-58-06.png)

Targetを図のような対応になるように設定します。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-02-24.png)

設定できたら、[Show Advanced]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-14-09.png)

Targetを図のような対応になるように設定します。
右手はとくに間違えやすいので、よく確認しながら設定しましょう。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-13-29.png)

[Save]ボタンからMapping情報を保存しておくと、[Load]ボタンから同じ設定を読み込むことができます。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-16-30.png)


### SK_MannequinのSet up Rigを設定する

「SK_Mannequin」側のSet up Rigを設定します。
「SK_Mannequin」を開きます。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-20-48.png)

「Retarget Manager」を開き、[Set up Rig]カテゴリーの[Slect Rig]に[Humanoid Rig]を設定します。
こちらは自動的に設定されますので、変更しません。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-20-32.png)


### SK_MannequinのBasePaseをTPoseにする
「SK_Mannequin」と「SK_PlaskMannequin」でBasePoseが異なります。
このままリターゲットを行うと、Motionが壊れてしまいます。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-24-02.png)

AnswerHubで「SK_Mannequin」をT-PoseにしたMotionFBXをダウンロードできるようにしてくれていました。
https://answers.unrealengine.com/questions/289404/t-pose-for-ue4-new-mannequin.html

![](/images/articles/plask-to-unrealengine/2022-01-19-22-25-11.png)

ダウンロードした「T_Pose_UE4_Mannequin.FBX」を「Animations」フォルダにImportします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-27-34.png)

[Skelton]に[UE4_Mannequin_Skelton]を設定します。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-28-40.png)

[Import]をクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-29-15.png)

「T_Pose_UE4_Mannequin」を右クリックし、Create > Create PoseAssetを選択します。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-30-17.png)

「T_Pose_UE4_Mannequin」を選択して、[Apply]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-31-07.png)

「Retarget Manager」の[Set up Rig]カテゴリーの [Modify]ボタンをクリックし、「T_Pose_UE4_Mannequin_PoseAsset」を選択します。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-40-39.png)

[Import]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-41-25.png)

ViewportのSK_MannequinがT-Poseになります。
もう一度[Modify]ボタンをクリックし、[Use CurrentPose]を選択します。
これで「SK_Mannequin」のBasePoseがA-PoseからT-Poseになり、「SK_PlaskMannequin」と同じT-Poseになりました。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-42-45.png)

### すべて保存する

ここで一度プロジェクトをすべて保存しましょう。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-37-36.png)


### Plaskのアニメーションをリターゲットする
「SK_Mannequin」のアニメーションであればどれでもいいのですが、
「T_Pose_UE4_Mannequin」を右クリックし、[Retarget Anim Assets] > [Duplicate Anim Assets and Retarget]を選択します。
![](/images/articles/plask-to-unrealengine/2022-01-19-23-44-39.png)

「SK_PlaskMannequin」を選択し、[Retarget]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-46-40.png)

Plaskで作成したMotionを右クリックし、[Retarget Anim Assets] > [Duplicate Anim Assets and Retarget]を選択します。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-36-21.png)

「UE4_Mannequin_Skelton」を選択し、[Retarget]ボタンをクリックします。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-47-51.png)

「Contents」フォルダ直下に、SK_MannequinにリターゲットされたPlaskのMotionが作成されます。
![](/images/articles/plask-to-unrealengine/2022-01-19-22-49-37.png)

これで、Plaskで作成したMotionがSK_Mannequinのような汎用的なモデルでも使用できます。


## まとめ
PlaskからMotionを作成するのに必要な機材は「**PCとWebカメラ**」です。
高精度と言う訳ではありませんが、手ごろな機材でこれだけの精度を出せるのがスゴイです。

手軽だからこそ、いままであったらいいなと思っていたことができます。

- 意識合わせ
- 静止画のポーズ付け

Motionのコンテ代わりに使えるのが大きいのではないでしょうか。

人工知能と仲良くならないと！


