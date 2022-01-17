---
title: "ポジTAのZenn設定【執筆、Github連携、VSCode拡張】"
emoji: "🦾"
type: "tech" # tech: 技術記事 / idea: アイデア
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

## GitHub連携について

### GitHub連携について(公式)
Zenn公式が分かりやすい説明を掲載しています。

https://zenn.dev/zenn/articles/connect-to-github

ポジTAは途中からの連携なので、こちらを参考にさせていただきました。
https://zenn.dev/zenn/articles/setup-zenn-github-with-export

### GitHubのZennリポジトリ名について
Zennのコンテンツを管理するリポジトリ名を決める時に参考にさせていただきました。
https://zenn.dev/j5c8k6m8/articles/zenn-github-repository-name

ポジTAのZennGitHubリポジトリは「**posita33-zenn-contents**」で管理します。
https://github.com/posita33/posita33-zenn-contents

branch名は[**main**]から[**zenn**]に変えて管理することにしました。

![branchの名前をzennに変える](/images/zenn_github_and_vscode_setup/2022-01-17-17-03-03.png)


## ZennをVSCodeで執筆するための拡張(Expression)設定

### 執筆を高速化する設定
VSCodeの拡張(Expression)設定を参考にさせていただきました。
https://zenn.dev/ctrlkeykoyubi/articles/e7d91c5286a409

**InstallしたVSCode拡張(Expression)**
- Paste Image
- Zenn Editor
- Excel to Markdown table
- Markdown All in One

**ショートカットが分からずハマったところ**
Paste Image拡張機能のペーストショートカット
**Ctrl + Alt + V**
(Ctrl + Vでは画像のコピーとMarkdown文がペーストされない)

Excel to Markdown table拡張機能のショートカット
**Alt + Shift + V**

Markdown All in One拡張機能で整形するショートカット
**Alt + Shift + F**

![](/images/zenn_github_and_vscode_setup/2022-01-17-17-16-09.png)


### 文章校正を効率化する(textlint、テキスト文章校正くん)
Webの文章校正ツールを使って文章校正していました。
https://note.com/posi_ta/n/n3134dbf8a638

ローカルのMarkdownファイルで記事を書いていくので、便利な文章校正が無いか探したら見つかりました。
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
![](/images/zenn_github_and_vscode_setup/2022-01-17-17-56-53.png)

## 随時最適化
書きながら改善した内容を記録していきます。

