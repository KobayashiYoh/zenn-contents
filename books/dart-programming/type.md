---
title: "型と変数"
---

## この章で学ぶこと
変数とは、データを入れておくための箱のようなものです。
変数はプログラム内で情報を保存し、必要なときにその情報を利用するために使用されます。

## 変数の定義
変数を作ることを、変数の定義と言います。
さっそく変数を定義していきましょう。
変数は、以下のような形式で定義することができます。
```
型 変数名;
```

これだとイメージがしづらいと思うので、サンプルコードを見てみましょう。
intが型、ageが変数名に該当します。
```dart
void main() {
  int age;
}
```

## 型
型とは、プログラムで扱うデータの種類のことです。型には様々な種類がありますが、Dartでよく利用される代表的なものを載せておきます。
| 型名 | 型の役割 | 具体例 |
| --- | --- | --- |
| int | 整数 | 10, 0, -3など |
| double | 小数 | 10.0, 0.0, -0.3など |
| String | 文字列 | ‘Hello, world’, ‘こんにちは’など |
| bool | 真か偽か | true, false |

それぞれの型については、後で詳しく解説します。
## 変数名
変数名とは、変数につける名前のことです。
変数名は基本的に自分で自由に決めることができます。しかし、自由に決めることができるからと言って、なんでも良いというわけではありません。一目でどんな役割を持った変数なのか判断できるような名前をつけるように心がけましょう。
```dart
// BAD

// 変数名がnだと、nがどんな値を扱っている変数なのかわからない
int n;

// 何かのカウント数を表す変数であるということはわかるが、何のカウント数なのかはわからない
int count;
```

```dart
// GOOD

// 変数名がstudentNumberであることから、この変数が扱っているのが学籍番号であるということがわかる
int studentNumber;

// 変数名がlikesCount（いいね）であることから、この変数はいいねの数をカウントしていることがわかる
int likesCount;
```
また、変数名には命名規則があります。
複数の単語を組み合わせて変数名を考える場合、`studentNumber`や`likesCount`のように、キャメルケース（camelCase）で最初の単語の先頭は小文字、2つ目以降の単語の先頭は大文字になるようにしてください。

## 代入
変数は定義しただけだとただの空箱のようなものです。
代入をして変数の中に値を入れてみましょう。
`=`を使って変数に値を代入することができます。
```dart
void main() {
  int age;
  age = 19;  // int型の変数ageに19を代入
  print(age);
}
```

また、変数宣言時に値を代入することもできます。
```dart
void main() {
  int age;
  age = 19;  // int型の変数ageに19を代入
  print(age);
}
```

## int型
ここまでで散々登場してきましたが、int型は整数を扱う型です。
整数の数値のみ扱うため、int型の変数に小数を含む値を代入することはできません。
```dart
int pageCount = 3;
int friendCount = 0;
int temperature = -3;
```

## double型
double型は小数を扱う型です。
数値の整数部分だけでなく、小数部分も扱うことができます。
```dart
double a = 8.25;
double b = 0.0;
double c = -8.25;
```

## String型
String型は文字列を扱う型です。
Dartでは、`’`（シングルクォーテーション）で囲んだ文字をString型の値として扱うことができます。実は、第1章で登場した`print(’Hello, world!’);`の`’Hello, world!’`はString型の値です。String型では、英数字記号に加え、日本語も扱うことができます。
```dart
String message = 'Hello, world!';
String companyName = '株式会社Shinonome';
String hashtag　= '#mobile';
```
以下のように`$`を使うと、文字列と文字列を連結させることができます。
```dart
void main() {
  String lastName = '東雲';
  String firstName = 'たま';
  String fullName = '$lastName$firstName';
  print(fullName);
}
```

以下のように`$`や`${}`を使うと、int型やdouble型の値を文字列に埋め込むこともできます。
```dart
	int age = 25;
  double height = 1.75;

  String ageString = '$age歳'; // int型をstring型に変換
  String heightString = '${height}cm'; // double型をstring型に変換
```

## bool型
bool型は`true`と`false`の2つのみを扱う型です。
bool型として扱える値は`true`（真）と`false`（偽）の2つのみです。
```dart
bool isLoading = true;
bool hasError = false;
```
「こんなことができて何が楽しいのか」と思われたかもしれませんが、bool型はプログラミングにおいてとても重要な役割を果たします。
詳しくは、[第4章「条件分岐」](https://www.notion.so/4-8929e84f6434447f87e5e04aa921133e?pvs=21) で解説するのでお楽しみに。

## DateTime型
DateTime型は、その名の通り日時を扱う型です。
`year, month, day, hour, minute, second, millisecond, microsecond`をコンマ区切りで順番に指定することで、日時を表現することができます。
これらを全てを入力する必要はありませんが、`year`だけは省略できないので注意してください。
```dart
DateTime birthday = DateTime(2016, 8, 25);
```
`.`を使うことで、`year, month, day, hour, minute, second, millisecond, microsecond`をそれぞれint型の値として使うことができるようになります。
```dart
DateTime birthday = DateTime(2016, 8, 25);
int birthMonth = birthday.month;
```

## const
プログラム内で変更されずに一定の値を持つ変数のことを定数と呼びます。
変数を宣言する際、変数の型の前に`const`をつけることで、その変数を定数として扱うことができます。
```dart
const double pi = 3.14;
```
定数は値を変更することができないため、誤った値の代入を防ぐことができます。
```dart
// BAD
const double pi = 3.14;
pi = 3;
```

## null
値が存在しないことを表す特殊な値のことを`null`と言います。
変数に値が何も代入されていない場合、その変数は`null`となります。
通常、Dartでは、NullSafetyと呼ばれるルールによって、変数に何も代入しない（= 変数がnullになること）を禁止されています。
しかし、変数を宣言する際、型の直後に?をつけることで、nullを許容することができるようになります。
```dart
// BAD
// userIdがString型であるのに対し、何も代入されていない（=null）であるため、エラーが発生する。
String userName;
print(userName);

// GOOD
// userIdがString?型であるため、nullを許容することができる
String? userName;
print(userName);
```
