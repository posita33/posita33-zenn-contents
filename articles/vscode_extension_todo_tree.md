---
title: "TODO検索できるVS Code拡張「Todo tree」 忘れないうちにTODOを残そう"
emoji: "🦉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["vscode", "markdown"]
published: true
---

## 忘れないうちにTODOを残す

Javaを書いていた時の習慣で、TODOコメントを残しています。
あとで「TODO」を全体検索で探せばいいかと考えていていました。
EclipseはTODOがリスト化されて、TODOをクリックすれば該当箇所に飛べたので便利でした。

**「VS CodeだからExtensionがあるのではないか？」**

探してみたら「Todo Tree」というExtensionがありましたのでご紹介します。

![](/images/articles/vscode_extension_todo_tree/2022-02-04-06-17-50.png)


## VS CodeでTODOをリスト化してくれるExtension「Todo Tree」

https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree

Extentionの検索バーに「TODO Tree」と検索してインストールします。
インストール後にはVS Codeの再起動が必要です。

![](/images/articles/vscode_extension_todo_tree/2022-02-04-06-06-28.png)

左側に「Todo Tree」アイコンが追加されるのでクリックします。
TODOを書いたファイルとTODOの箇所がリストで表示されます。
TODOの行をクリックすると該当箇所に飛ぶことができます。
TODOの箇所の背景色が見やすくなっているので気付きやすくなります。

![](/images/articles/vscode_extension_todo_tree/2022-02-04-06-14-05.png)

## 他にも使えるタグ

`TODO`以外にも使用できるタグがあります。
Todo Treeのアイコンもタグごとに違います。

```
BUG
HACK
FIXME
XXX
[ ] 項目（未完了）
[x] 項目（完了）
```

![](/images/articles/vscode_extension_todo_tree/2022-02-11-12-52-48.png)

項目をリスト化するとチェックボックスで管理できるので便利です。

```
- [ ] 項目（未完了）
- [x] 項目（完了）
  - [ ] サブ項目（未完了）
  - [x] サブ項目（完了）
```

![](/images/articles/vscode_extension_todo_tree/2022-02-11-12-54-30.png)

Todo Treeで監視できるタグは[Todo-tree > General: Tags]から追加できます。

![](/images/articles/vscode_extension_todo_tree/2022-02-11-12-59-04.png)

## まとめ

TODOを書くと汚くなってしまうけど、気付いた時に直せないなら汚いものを残して必ず直す決意を持たせることが必要です。
あとでやろうは信じてはいけない。
あとで絶対直さなきゃにすると、未来の自分が息抜きに直してくれます。
