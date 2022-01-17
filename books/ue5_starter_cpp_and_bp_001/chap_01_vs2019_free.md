---
title: "1.4. 有料Extensionを使用しない VisualStudioの設定"
free: false
---

Visual Assistを使用する場合は、Intellissenceをオフにしているのでエラーは表示されません。
次の項目にお進みください。

## 有料Extensionを使用しない VisualStudioの設定
最初にVisualStudioが大量のエラーが出ているのは、Intellisenceがヘッダーファイルを見に行っているけど、見つからないから発生しているエラーです。
![](https://storage.googleapis.com/zenn-user-upload/5221c310d098-20220110.png)

プロジェクトファイルの設定を直すことでエラーを消すことが出来ます。
今回のエラーはIntellisenseがヘッダーを開けないので、IncludeSearchPathを設定することでエラーを消すことが出来ます。

プロジェクトファイルのプロパティを開きます。
プロジェクトファイルを右クリック > Properties
![](https://storage.googleapis.com/zenn-user-upload/f36a5cea34b3-20220110.png)

Include Search Pathを追加することで直ります。
UE4のInclude Search Pathの一覧がGithubで提供されていました。
UE5 EAでは「UE4Editor」というフォルダ名が「UnrealEditor」に変更されているので、置換したファイルをGithubに公開しました。
https://gist.github.com/posita33/c639a0d558d4332478df506b5ec773d2#file-includepaths_ue5ea-txt

※UE4で編集する場合（元ネタ）
https://gist.github.com/Jakob-PB/a9ea415f4d9d0189926429cbd0242cef#file-includepaths-txt

Rawボタンをクリックして、全体を選択してからコピーします。
![](https://storage.googleapis.com/zenn-user-upload/f12d0eb457ac-20220110.png)

NMakeのIntellisence > Include Search Pathにペーストします。
![](https://storage.googleapis.com/zenn-user-upload/576d878372df-20220110.png)

大量にあったエラーが消えます。

https://twitter.com/posita33/status/1471717823580098563

次にオプションの設定を行います。
Tools > Options…
![](https://storage.googleapis.com/zenn-user-upload/1430d58c190d-20220110.png)

Text Editor C/C++のIntelliSenceの設定を変更します。
![](https://storage.googleapis.com/zenn-user-upload/d162c47cb83f-20220110.png)

【参照URL】
https://www.youtube.com/watch?v=ap9snUkchmY

https://www.youtube.com/watch?v=vODHoUT5URs

