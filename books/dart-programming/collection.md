---
title: "コレクション"
---

## コレクションとは
「コレクション」とは、複数の値をまとめて管理することです。
あなたは現実世界で何かコレクションを持っていますか？アニメやゲームの作品、スポーツやアイドルといった趣味、旅行先のお土産などなど、何かしらのグッズを集めたことがある方が多いのではないでしょうか。その際、複数のグッズを1つのコレクションとしてまとめると思います。
現実世界と同じように、プログラミングにも複数の値をまとめて管理するコレクションと呼ばれる仕組みが用意されています。前章で紹介したint型やString型などの変数では、1つの変数につき1つの値しか格納することができませんでした。しかし、コレクションを使って変数を定義することにより、1つの変数に複数の値を格納することができるようになります。
本章では、DartのコレクションであるListとSetとMapの3つについてご紹介します。

## Listとは
Listとは、名前の通り複数の値を順番にまとめて格納するためのコレクションです。
Listでは、`[]`の中に複数の値を`,`で区切ってまとめて管理します。このとき、List内に格納されているそれぞれの値のことを「要素（element）」と呼びます。
また、Listは型として使うことができます。`List<型名>`のように、`<>`内に格納したい値の型を指定することで、Listを型として使うことができます。
では、実際にListを使ったのサンプルコードを見てみましょう。
```dart
void main() {
	// int型のListであるscoresを定義
  List<int> scores = [97, 56, 43, 82, 90];
  print(scores);
}
```
上記のコードでは、List<int>型の変数scoresを定義し、List<int>型の値である`[97, 56, 43, 82, 90]`を代入しています。
scoresは変数なので、型と実際に代入される値の型が同じである必要があります。scoresはList<int>型、すなわちint型の値を格納するListの変数であるため、代入する右辺のList内にある値も全てint型の値である必要があります。
そのため、次のようにList<int>型の変数scoresにList<String>型の値（=文字列のList）を代入することはできません。
```dart
// Error
List<int> scores = ['S', 'E', 'E', 'A', 'S'];

// OK
List<String> scores = ['S', 'E', 'E', 'A', 'S'];
```
ここまで見てきたように、Listを使うと`[]`内に複数の値を`,`区切りでまとめて格納することができます。また、`List<型名>`でListに格納したい値の型名を指定することで、変数として定義することもできます。

## Listの添え字
Listの添え字を使うことで、Listから値を取り出すことができます。
Listでは、複数の値を「順番に」まとめて管理しています。List内の値は0, 1, 2, 3, …と順にそれぞれ番号が割り振られています。その割り振られた番号のことを「添え字（index）」と呼びます。添え字は整数の番号なので、int型になります。
ここで注意が必要なのが、添え字が「1からではなく0から順に割り振られる」という点です。例えば、添え字`0`を指定するとList内の1番目の値を取り出すことができますし、添え字`2`を指定すると、List内の3番目の値を取り出すことができます。このように、添え字は1からではなく0から順に割り振られるため、取り出したい順番と添え字は1つずつずれることになります。
それでは、実際にサンプルコードで添え字を使ってListから値を取り出してみましょう。

```dart
void main() {
  List<int> scores = [97, 56, 43, 82, 90];

  // 添え字0を使ってListの1番最初の値を取り出す
  print(scores[0]);

  // 添え字2を使ってListの3番最初の値を取り出す
  print(scores[2]);
}

```
このように、Listの変数の後ろにある`[]`内に添え字を指定することで、List内の値を取り出すことができます。

## List操作
Listに要素を追加したり、削除したりすることができるList操作について紹介します。
List操作には様々な種類たありますが、ここで紹介するのはList操作の一部になります。
`add`を使うと、Listの一番後ろに要素を追加することができます。
```dart
 	// Listの一番後ろに要素を追加
  List<int> scores = [97, 56, 43, 82, 90];
  scores.add(100);
  print(scores);
```

- 実行結果
    
    ```
    [97, 56, 43, 82, 90, 100]
    ```
    

`addAll`を使うと、Listの一番後ろにListの全要素を追加することができます。
```dart
  // Listの一番後ろにListの全要素を追加
  List<int> scores = [97, 56, 43, 82, 90];
  List<int> newScores = [100, 77, 60];
  scores.addAll(newScores);
  print(scores);
```

- 実行結果
    
    ```
    [97, 56, 43, 82, 90, 100, 77, 60]
    ```

`clear`を使うと、Listの要素を全て削除することができます。

```dart
  // Listの要素を全て削除
  List<int> scores = [97, 56, 43, 82, 90];
  scores.clear();
  print(scores);
```

- 実行結果
    
    ```
    []
    ```
    

`length`を使うと、Listの要素数を求めることができます。

```dart
// Listの要素数を求める
List<int> scores = [97, 56, 43, 82, 90];
print(scores.length);
```

- 実行結果
    
    ```
    5
    ```
    

## Setとは
Setとは、Listの重複禁止バージョンです。Listは同じ値を複数格納することができましたが、Setは同じ値を複数格納することができません。
それでは、実際にSetを利用している例を見てみましょう。

```dart
Set<int> scores = {97, 56, 43, 82, 90};
```

- 実行結果
    
    ```
    {97, 56, 43, 82, 90}
    ```
    
上記のコードでは、先ほどのListのサンプルコードと同じように値をカンマ区切りで格納しています。
カンマ区切りで値を入れていくという点はListと同じです。しかし、Listは格納する値を`[]`で囲んでいましたが、Setは格納する値を`{}`で囲んでいます。
また、先述したように、Setには重複する値を格納することはできません。
実際にサンプルコードを書いてみて確かめてみましょう。
```dart
void main() {
  Set<String> seasons = {'春', '夏', '秋', '冬', '春'};
  print(seasons);
}

```

- 実行結果
    
    ```
    Two elements in a set literal shouldn't be equal.
    ```
    
エラーが発生してしまいます。
このように、Listには重複する値を複数格納することができるのですが、Setでは重複する値を格納することができません。
これがListとSetの違いになります。

## Mapとは
Mapとは、複数の値を「キー」と「バリュー」のペアで保管することができるコレクションのです。
Listは複数の値を添字とバリューのペアで保管しましたが、Mapはキーとバリューのペアで保管します。
それでは、実際にMapを利用している例を見てみましょう。
```dart
void main() {
  Map<String, String> languages = {
    'ja': '日本語',
    'en': 'English',
  };
  print(languages['ja']);
  print(languages['en']);
}

```

- 実行結果
    
    ```
    日本語
    English
    ```
上記のコードでは、Map<String, String>型のMapであるlanguagesにそれぞれキーとバリューを格納しています。
Mapでは、{}の中にカンマ区切りで、`{キー: バリュー}`の形式になるようキーとバリューのペアを格納していきます。
Map<String, String>では、Mapのキーとバリューの型を指定しています。今回、キーもバリューも両方String型で宣言しているため、languagesに格納されるキーもバリューもString型である必要があります。