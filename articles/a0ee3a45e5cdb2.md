---
title: "【C++＆BP Column】エラーメッセージが起きた時の対処方法 Compilerは間違いを教えてくれる友達"
emoji: "🤝"
type: "tech"
topics: ["cpp", "unrealengine", "ue4", "ue5"]
published: true
---

## Compileでエラーメッセージが出た時の対処方法

### エラーメッセージ出たら慌てない
Compileをしていたら、エラーが出てしまいました！

**どーしよー！**

まずは、慌てずに**エラーメッセージを確認しましょう。**
![](https://storage.googleapis.com/zenn-user-upload/80cee07cdefc-20220114.png)

### エラーメッセージを検索する
エラーメッセージをコピーして、検索エンジンの検索欄にエラーメッセージをペーストして検索します。
エラー番号を含めておくと、コンパイルエラーの原因であるページが見つかります。
後はページに移動してエラーの原因を把握します。

UnrealEngineの場合は「UE4 エラーメッセージ」もおススメです。

![](https://storage.googleapis.com/zenn-user-upload/cb4547d68d66-20220114.png)

https://docs.microsoft.com/ja-jp/cpp/error-messages/compiler-errors-1/compiler-error-c2166?view=msvc-170

### エラーメッセージを翻訳する
エラーメッセージをGoogle翻訳で翻訳することで意味を把握します。
![](https://storage.googleapis.com/zenn-user-upload/16e2a245d53e-20220114.png)

### AnswerHubで質問を検索する
UnrealEngineではAnswerHubという質問できるコミュニティがあります。エラーメッセージを検索することで、過去に同じエラーメッセージに悩まされた人たちのやり取りを見ることが出来ます。
![](https://storage.googleapis.com/zenn-user-upload/b50c4a0b523e-20220114.png)

## エラーメッセージは友達
エラーメッセージが出たら**エラーを直せばいい**だけです。

コンパイラはエラーだと教えてくれるソースコードを書く上での友達です。

本当に怖いのは**エラーを黙って裏で笑っている友達**です。

**お前間違っているよ！**

**自分の間違いを教えてくれる友達**は大切にしましょう。

