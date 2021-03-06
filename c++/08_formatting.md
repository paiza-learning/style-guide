# フォーマッティング

## ツール

`clang-format` を利用します.

これにより, インデント, 型の一部の `&`, `*` などの位置, 波かっこ前の改行などが指定されます. これを適用するには, `clang-format` をインストールし, プロジェクトのルートに [`.clang-format`](./.clang-format) を置き, 以下のように実行してください.

```sh
# `-i` オプションを指定することでスタイルを適用したコードに書き換えます.
$ clang-format -i filename.cpp
```

現在, フォーマットの指定は [`.clang-format`](./.clang-format) に指定されたものを利用します. これはほとんどが Google スタイルの流用です.

以下には [`.clang-format`](./.clang-format) に指定されないルールを記述しています.

## [強制] if や while のブロックの波括弧は毎回書く

短く書けるならば短く書くのがよいのですが, スタイルを合わせるためにこれらは毎回ブロックとして書いてください.

```c++
if (a == b) break; // never

if (a == b) {      // good
  break;
}
```

## [推奨] 桁区切りできるならする

```c++
1'000'000'009 // ok
1000000009    // 分かりにくい
```

## [推奨] enum の最後の要素には `,` を付ける

次のように書くと, フォーマッタにより一行に整形されることがあります (幅によります).

```c++
// こう書くと
enum direction {
  UP,
  DOWN,
  LEFT,
  RIGHT
};

// ↓ のようになる
enum direction { UP, DOWN, LEFT, RIGHT };
```

これを避けるには, 最後の要素の後にも `,` を打てばよいです.

```c++
// そのまま改行が維持される
enum direction {
   UP,
   DOWN,
   LEFT,
   RIGHT,
};

// 逆に ↓ のように書くと ↑ のように整形される
enum direction { UP, DOWN, LEFT, RIGHT, };
```
