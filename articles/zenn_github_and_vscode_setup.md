---
title: "ポジTAのZenn設定"
emoji: "⚙️"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["zenn", "vscode", "github"]
published: true
---

## 執筆する際に覚えておくこと

【Markdown記法一覧】
https://zenn.dev/zenn/articles/markdown-guide

【Bookのチャプターファイルの作成方法】
config.yamlでmdファイルの並び順を設定できる。
https://zenn.dev/zenn/articles/deprecated-book-deployment

【使える絵文字一覧】
articleに使用する絵文字一覧
https://getemoji.com/

## アクセス解析
Googleアナリティクスの設定はこの記事を参考にさせていただきました。
https://zenn.dev/masakiyo/articles/76ca3b774c6746

## GitHub連携について

### GitHub連携について(公式)
Zenn公式が分かりやすい説明を掲載しています。

https://zenn.dev/zenn/articles/connect-to-github

ポジTAは途中からの連携なので、こちらを参考にさせていただきました。
https://zenn.dev/zenn/articles/setup-zenn-github-with-export

### GitHubのZennリポジトリ名について
Zennのコンテンツを管理するリポジトリ名の参考にさせていただきました。
https://zenn.dev/j5c8k6m8/articles/zenn-github-repository-name

ポジTAのZennGitHubリポジトリは「**posita33-zenn-contents**」で管理します。
https://github.com/posita33/posita33-zenn-contents

branch名は[**main**]から[**zenn**]に変えて管理することにしました。

![branchの名前をzennに変える](/images/articles/zenn_github_and_vscode_setup/2022-01-17-17-03-03.png)
*branch名を編集する手順*

### 公開リポジトリにする際のライセンス設定について
営利目的の使用を禁止にしておきたかったので、
CC BY-SAで運用することにしました。(2021/1/22)
https://creativecommons.org/licenses/by-nc/4.0/deed.ja

CCライセンスの設定についてはコチラの記事を参考にさせていただきました。
https://zenn.dev/spiegel/articles/20200919-ccl


## ZennをVS Codeで執筆するための拡張(Expression)設定

### 執筆を高速化する設定
VS Codeの拡張(Expression)設定を参考にさせていただきました。
https://zenn.dev/ctrlkeykoyubi/articles/e7d91c5286a409

https://zenn.dev/nkys39/articles/struct-zenn-win10

**InstallしたVS Code拡張(Expression)**
- Paste Image
- Zenn Editor
- Excel to Markdown table
- Markdown All in One
- CharacterCount
- Git Graph

:::details ショートカットが分からずハマったところ  

**ショートカットが分からずハマったところ**
Paste Image拡張機能のペーストショートカット
**Ctrl + Alt + V**
(Ctrl + Vでは画像のコピーとMarkdown文がペーストされない)
:::

:::details Paste Imageの設定方法
**Paste Imageの設定方法**
Paste Imageの設定はコチラの記事の方が分かりやすい
https://zenn.dev/waddy/articles/image-paste-zenn-upload

画像保存フォルダを[articles]を[books]で分けるようにワークスペースを別々にした。
| ワークスペース名             | Paste Image : Path                       |
| ---------------------------- | -------------------------------------- |
| article.code-workspace       | images/articles/(画像ファイル名)       |
| book-(book名).code-workspace | images/books/(book名)/(画像ファイル名) |
:::

:::details 表を作る時のショートカット

Excel to Markdown table拡張機能のショートカット
**Alt + Shift + V**

Markdown All in One拡張機能で整形するショートカット
**Alt + Shift + F**

![](/images/articles/zenn_github_and_vscode_setup/2022-01-17-17-16-09.png)
*連携することでキレイな表が書ける*
:::

:::details Git Graphの表示について
Git Graphをインストールしても、どこから見たら分からなかったです。

図のようにソース管理に移動して、Git Graphアイコンをクリックすると見られます。
![](/images/articles/zenn_github_and_vscode_setup/2022-01-19-06-00-56.png)
:::

### 文章校正を効率化する(textlint、テキスト文章校正くん)
Webの文章校正ツールを使って文章校正していました。
https://note.com/posi_ta/n/n3134dbf8a638

:::details VS Codeの文章校正
ローカルのMarkdownファイルで記事を書いていくので、便利な文章校正を探したら見つかりました。

https://zenn.dev/appgrape/articles/textlint-setting

**他にもプリセットを入れたい時の設定**
https://qiita.com/takasp/items/22f7f72b691fda30aea2

**textlint作者のazuさんページ**
https://efcl.info/2015/09/10/introduce-textlint/


textlintの設定は少し難しいので、「テキスト校正くん」という拡張がありました。
https://marketplace.visualstudio.com/items?itemName=ICS.japanese-proofreading

ら抜き言葉といった言葉遣いを波線で教えてくれます。
✕食べれる
〇食べられる
![](/images/articles/zenn_github_and_vscode_setup/2022-01-17-17-56-53.png)

テキスト校正くんでチェックを外した設定です。
![](/images/articles/zenn_github_and_vscode_setup/2022-01-25-22-26-59.png)

:::

### 文字数をカウント

アウトプットビルディングのために文字数が何文字か知りたいので、「**CharacterCount**」をインストールしました。
https://marketplace.visualstudio.com/items?itemName=8amjp.charactercount

![CharacterCount](/images/articles/zenn_github_and_vscode_setup/2022-01-17-18-34-48.png)
*左下に文字数が表示される*

画像のパス文字列までカウントしてしまうので、「簡単文字数カウント」Google Chrome拡張からPreviewページをカウントしている。
https://chrome.google.com/webstore/detail/%E3%81%8B%E3%82%93%E3%81%9F%E3%82%93%E6%96%87%E5%AD%97%E6%95%B0%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88/lmmephjlhfdnijfigajbmemendbfhnha


### よく使うMarkdown記法のSnippet登録

アコーディオンを使いたかったので調べてみたら、他にも使えそうなMarkdown記法がありました。
よく使うMarkdown記法も一緒に追加しました。

https://zenn.dev/posita33/articles/zenn_markdown_snippet
(2022/1/18)

## 随時最適化
書きながら改善した内容を記録します。

