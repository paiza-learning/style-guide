# 07. 言語機能

## [回避] マクロを避ける

`REP` マクロなどを競技プログラミングではよく見かけますが、paiza ラーニングの模範解答欄にパーソナライズドされがちなものが載ってしまうと問題かと思います。

定数は `constexpr` 等で定義できることかと思います。

## [推奨] キャストの形式

キャストは C 形式を使わずに, 関数形式、または名前付きキャストにしてください。

```c++
auto i = (int) d; // bad
auto i = int(d);  // good
auto i = static_cast<int>(d); // best
```

## [推奨] typedef は using にする

積極的に `using` を利用します.

```c++
typedef long long ll; // bad
using ll = long long; // good

typedef int (*f)(double, string);  // bad
using f = int (*)(double, string); // good
```

## [推奨] range-based for、構造化束縛などは積極的に用いる

paiza の clang++ は c++20 なのでそこまで利用できるものならば活用しましょう。

```c++
for (const auto& [x, y] : points) { /*...*/ }
```

## [回避] auto ... -> ret_type で `main` 関数を定義するのは避ける

基本的には意味がないので利用しません.

```c++
int main() { return 0; }         // good
auto main() -> int { return 0; } // bad
```

## [回避] 条件式を複雑にしない

複雑なものは分割して変数に避けるなどします.

```c++
if (a == b && (b != c % 4 || d + c / 4 != e) && e * f <= 4) // should avoid

bool some_flag = a == b && (b != c % 4 || d + c / 4 != e) && e * f <= 4; // mmm
if (some_flag)

bool some_flag_what = a == b;
bool some_flag_oops = b != c % 4 || d + c / 4 != e;
bool some_flat_whoa = e * f <= 4;
if (some_flat_what && some_flag_oops && some_flag_whoa) // good
```

## [回避] ネストを深くしない (早期 return などを使う)

```c++
// bad
if (a) {
  if (b) {
    if (c) {
      cout << "reached" << endl;
    } else {
      cout << "so close" << endl;
    }
  }
}

// better
if (!a) return;
if (!b) return;
if (c) {
  cout << "reached" << endl;
} else {
  cout << "so close" << endl;
}
```

## [推奨] 真偽値には int ではなく bool を用いる

```c++
while (1)    // うーん
while (true) // ok
```

## [回避] true/falseが1/0として解釈されることを利用するのは避ける

```c++
int a[n];

// bad
for(int i = 0; i < n; i++){
  cout << a[i] << " \n"[i==n-1];
}

// good
for(int i = 0; i < n; i++){
  cout << a[i];
  if(i != n-1)  cout << " ";
  else          cout << endl;
}
```

## [強制] 偶奇判定に &1 をつかわない

剰余をとるという話であれば, すなおに `%` しましょう

```c++
if (i % 2 != 0) // good
if (i & 1)      // avoid
```

## [推奨] データはまとめる (めんどくさくない程度に)

座標を `x`, `y` のようにバラして扱うより, `pair` や `tuple` のように意味のあるかたまりとして纏めることを推奨します.

三次元座標であれば `tuple<int, int, int>` のようにして扱うことができます.
