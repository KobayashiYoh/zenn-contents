---
title: "オブジェクト指向"
---

## この章で学ぶこと
オブジェクト指向を理解すると10,000行のコードも難なく書けるようになります。
今みなさんが書いているDartのコードは数十行ほどだと思いますが、実際のFlutterのアプリ開発だとコードを書く量が1,000行を超えるのは当たり前、10,000行に達することも珍しくありません。
膨大なコードの量に対して不安を感じてしまうかもしれませんが、安心してください。
それだけ大量なコードを書く必要があるにもかかわらず、世界中で100万種類以上のアプリがリリースされています。
なぜでしょうか？
その秘密がオブジェクト指向には隠されています。

## オブジェクト指向
オブジェクト指向とは、簡単に言うと「複雑な概念をラクに理解するための考え方」のことです。
オブジェクト指向を使いこなせるようになるとプログラミングがラクになります。
アプリ開発のために数千、数万行のコードを書くことができるのも、このオブジェクト指向を使っているからです。
つまり、オブジェクト指向を理解して使いこなすとラクにコードが書けるようになるのです。
この章では、クラスやインスタンスを始めとしたオブジェクト指向の様々な考え方を紹介していきます。

## クラスとインスタンス
クラスとインスタンスはよく「金型」と「たい焼き」の関係に例えられます。
クラスという1つの型を元に、複数のインスタンスを生成することができます。

## クラス
クラス（class）とは、「変数や関数をひとまとめにしたもの」です。
また、クラス内の変数のことをフィールド（field）、関数のことをメソッド（method）と言います。
クラスは以下のように書くことができます。

```dart
class クラス名 {
  // フィールドとやメソッドを定義する
}
```

`class`の後ろにクラス名をCamelCaseで書きます。
クラス名の後ろの{}内にフィールドやメソッドを定義していきます。
では、実際にたい焼きを表すTaiyakiクラスを作ってみましょう。

```dart
class Taiyaki {
  String type = 'あんこ';
  int price = 400;
}

void main() {}
```

- 実行結果
    
    ```
    
    ```
    
String型のフィールドtypeとint型のフィールドpriceを持ったクラスで、それぞれ`’あんこ’`と`400`という値を持っています。
しかし、これでコードを実行しても何も起きません。
関数と同じでクラスも定義しただけでは利用できないため、インスタンスを生成する必要があります。

## インスタンス
インスタンス（instance）とは、「クラスの情報を元に生成されるコピーのようなもの」です。
インスタンスは以下のように生成することができます。
```dart
クラス 変数名 = クラス();
```
クラスは型に例えられるように、実際に型として使用することができます。
インスタンスを代入する変数名はクラス名にちなんだ名前を付けることが多く、Taiyakiクラスのインスタンス
以下は先ほどのTaiyakiクラスのインスタンスを生成する例です。

```dart
class Taiyaki {
  String type = 'あんこ';
  int price = 400;

	void printType() {
    print('type: $type');
  }

  void printPrice() {
    print('price: $price');
  }
}

void main() {
  Taiyaki taiyaki = Taiyaki();
}
```

- 実行結果
    
    ```
    
    ```
    
たい焼きが作れましたね。
ここでは、Taiyaki型の変数taiyakiを定義し、Taiyakiインスタンスを代入しています。
また、1つのクラスさえあれば、以下のように複数のインスタンスを生成することも可能です。

```dart
class Taiyaki {
  String type = 'あんこ';
  int price = 400;

  void printType() {
    print('type: $type');
  }

  void printPrice() {
    print('price: $price');
  }
}

void main() {
  Taiyaki taiyaki1 = Taiyaki();
  Taiyaki taiyaki2 = Taiyaki();
  Taiyaki taiyaki3 = Taiyaki();
}
```
- 実行結果
    ```
    
    ```
たい焼きがたくさん作れましたね。
では、実際にインスタンスが生成できているかどうかprint文で確認してみましょう。

## フィールド
インスタンスの後ろに`.`を付けると、そのインスタンスのフィールド（クラス内に定義されている変数）の値を扱うことができます。
今回の例だと`taiyaki.type`で`’あんこ’`、`taiyaki.price`で`400`を利用することができます。
```dart
class Taiyaki {
  String type = 'あんこ';
  int price = 400;

  void printType() {
    print('type: $type');
  }

  void printPrice() {
    print('price: $price');
  }
}

void main() {
  Taiyaki taiyaki = Taiyaki();
	print('type: ${taiyaki.type}');
  print('price: ${taiyaki.price}');
}
```

- 実行結果
    
    ```
    type: あんこ
    price: 400
    ```
    

## メソッド
インスタンスの後ろに`.`を付けると、そのインスタンスのメソッド（クラス内に定義されている関数）を呼び出すことができます。
printTypeメソッドとprintPriceメソッドを呼び出してみましょう。

```dart
class Taiyaki {
  String type = 'あんこ';
  int price = 400;

  void printType() {
    print('type: $type');
  }

  void printPrice() {
    print('price: $price');
  }
}

void main() {
  Taiyaki taiyaki = Taiyaki();
  taiyaki.printType();
  taiyaki.printPrice();
}
```

- 実行結果
    
    ```
    type: あんこ
    price: 400
    ```
    

## コンストラクタ
現状だとあんこ味で400円のたい焼きインスタンスしか生成することができません。
毎日あんこ味のたい焼きだと飽きますよね。
1つのクラスから異なるフィールドのインスタンスを生成するためには、型であるクラスをどうにかする必要があります。
そこで役に立つのがコンストラクタ（constructor）です。
コンストラクタを使うと、引数として渡した値を元にインスタンス生成することができます。
引数に関しては、関数と同じように定義して値を渡すことができますが、引数の定義に`this`をつけ忘れないように注意してください。
`this`は同じクラス内の値を指しており、`this.type`はTaiyakiクラス内のString型フィールド`type`を、`this.price`はTaiyakiクラス内の`price`型フィールドを指しています。

```dart
class Taiyaki {
  Taiyaki({required this.type, required this.price});

  final String type;
  final int price;

  void printType() {
    print('type: $type');
  }

  void printPrice() {
    print('price: $price');
  }
}

void main() {
  Taiyaki taiyaki = Taiyaki(type: 'クリーム', price: 500);
  taiyaki.printType();
  taiyaki.printPrice();
}
```

- 実行結果
    
    ```
    type: クリーム
    price: 500
    ```
