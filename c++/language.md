# 言語機能

## マクロを避ける

`REP` マクロなどを競技プログラミングではよく見かけますが、paiza ラーニングの模範解答欄にパーソナライズドされがちなものが載ってしまうと問題かと思います。

定数は `constexpr` 等で定義できることかと思います。

## キャスト

キャストは C 形式を使わずに, 関数形式、または名前付きキャストにしてください。

```c++
auto i = (int) d; // bad
auto i = int(d);  // good
auto i = static_cast<int>(d); // best
```

## typedef は using にする

積極的に `using` を利用します.

```c++
typedef long long ll; // bad
using ll = long long; // good

typedef int (*f)(double, string);  // bad
using f = int (*)(double, string); // good
```

## range-based for、auto 宣言、構造化束縛などは積極的に用いる

paiza の clang++ は c++17 なのでそこまで利用できるものならば活用しましょう。

```c++
for (const auto& [x, y] : points) { /*...*/ }
```

## auto ... -> ret_type で関数を定義するのは避ける

基本的には全く意味がないので利用しません. ただし `decltype` などを利用するならば後置でよいです.

```c++
int main() { return 0; }         // good
auto main() -> int { return 0; } // bad
```
