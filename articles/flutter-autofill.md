---
title: "【Flutter】autofillHintsとAutofillGroupを用いてユーザー名とパスワードの自動入力機能を実装し、UXを向上させる方法"
emoji: "🧩"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [Flutter]
published: false
---

## はじめに
スマホを使っていると、iPhoneのTouch ID等でフォームのユーザー名やパスワードを自動入力できるアプリをよく見かけます。
ユーザー名とパスワードの入力する手間を省き、自動入力ができるようになれば、アプリのUXを向上させることができます。
そこで、今回はFlutterのautofillHintsとAutofillGroupを用いてユーザー名とパスワードを自動入力する方法についてご紹介させていただきます。

## 実装
### フォームのUIを組む
まず、自動入力の実装を行う前に、簡易的なフォームのUIを組みます。
今回は、以下のようなFormPageを作成します。
```dart

class FormPage extends StatefulWidget {
  const FormPage({super.key});

  @override
  State<FormPage> createState() => _FormPageState();
}

class _FormPageState extends State<FormPage> {
  final TextEditingController userNameController = TextEditingController();
  final TextEditingController passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: userNameController,
              decoration: const InputDecoration(
                label: Text('ユーザー名'),
              ),
            ),
            TextField(
              controller: passwordController,
              decoration: const InputDecoration(
                label: Text('パスワード'),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2017091/0975ae77-54ac-02a4-05f4-4c81a7aaa389.png" width="300">

これで、簡易的なフォームのUIを作成することができました。
しかし、Flutterでは、デフォルトだとユーザー名やパスワードを自動入力することはできません。
そこで、autofillHintsとAutofillGroupを活用します。

### autoFillHintsを追加
FlutterのTextFieldやTextFormFieldにはautoFillHintsと呼ばれるプロパティが用意されています。
このautoFillHintsを用いることで、Flutterでは自動入力を実現します。
ユーザー名を自動入力したい場合は`[AutofillHints.username]`を指定し、パスワードを自動入力したい場合は`[AutofillHints.password]`を指定します。
では、先ほど作成したフォーム画面のTextFieldにautoFillHintsを追加してみましょう。

```dart
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: userNameController,
              decoration: const InputDecoration(
                label: Text('ユーザー名'),
              ),
              autofillHints: const [AutofillHints.username],  // 追加
            ),
            TextField(
              controller: passwordController,
              decoration: const InputDecoration(
                label: Text('パスワード'),
              ),
              autofillHints: const [AutofillHints.password],  // 追加
            ),
          ],
        ),
```
ここまで実装できたら、実機で検証してみてください。
恐らく、ユーザー名とパスワードをそれぞれ自動入力できるようになっているはずです。
しかし、これだとユーザー名とパスワードをそれぞれ自動入力する必要があり、まだまだ手間がかかってしまいます。

### AutofillGroupを追加
ユーザー名とパスワードをまとめて自動入力するには、AutofillGroupというウィジェットで任意のTextFieldやTextFormFieldをまとめてラップする必要があります。
すると、AutofillGroup内が1つのグループとして認識され、AutofillGroup内のTextFieldやTextFormFieldをまとめて自動入力することができます。
```dart
        // 対象のTextFieldをまとめてwrapする
        child: AutofillGroup(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              TextField(
                controller: userNameController,
                decoration: const InputDecoration(
                  label: Text('ユーザー名'),
                ),
                autofillHints: const [AutofillHints.username],
              ),
              TextField(
                controller: passwordController,
                decoration: const InputDecoration(
                  label: Text('パスワード'),
                ),
                autofillHints: const [AutofillHints.password],
              ),
            ],
          ),
        ),
```
ここまでできたら、また実機で動作確認をしてみましょう。
ユーザー名とパスワードを自動入力できるようになっているはずです。

### コード全文
コード全文も載せておきます。
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const FormPage(),
    );
  }
}

class FormPage extends StatefulWidget {
  const FormPage({super.key});

  @override
  State<FormPage> createState() => _FormPageState();
}

class _FormPageState extends State<FormPage> {
  final TextEditingController userNameController = TextEditingController();
  final TextEditingController passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: AutofillGroup(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              TextField(
                controller: userNameController,
                decoration: const InputDecoration(
                  label: Text('ユーザー名'),
                ),
                autofillHints: const [AutofillHints.username],
              ),
              TextField(
                controller: passwordController,
                decoration: const InputDecoration(
                  label: Text('パスワード'),
                ),
                autofillHints: const [AutofillHints.password],
              ),
            ],
          ),
        ),
      ),
    );
  }
}

```

## さいごに
このように、FlutterのTextFormやTextFormFieldのautofillHintsを指定し、それらをAutofillGroupでラップすることにより、ユーザー名やパスワードといったフォームの自動入力機能を実装することができます。
ユーザー名やパスワードの自動入力機能を実装することで、ユーザーがキーボードで毎回入力する手間を省き、アプリのUXを向上させることができます。
ぜひ、自動入力機能を実装してみてください！
