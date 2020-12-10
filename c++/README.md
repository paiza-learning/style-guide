# c++ 模範解答コーディングルール

## 基準

- 強制
- 推奨
- 条件付推奨
- 許容
- 避ける
- してはいけない

基本的には STL/boost を意識して欲しい

## paiza ラーニングに特有の事情

これは paiza ラーニング模範解答として利用される場合に特有の事情で定められる規約です.

### `using namespace std;` は書く

paiza のスキルチェック問題等を C++ で解答する際, ほとんどの場合で STL を利用します.

こういった事情により, 毎回 `std::` を書いていては読みやすさが失われるため, これは書くものとします.

### コメントは書かない

コメントや各種の注意点などは別途用意される解説ファイルに記述します.

## 言語機能

### マクロを避ける

`REP` マクロなどを競技プログラミングではよく見かけますが、paiza ラーニングの模範解答欄にパーソナライズドされがちなものが載ってしまうと問題かと思います。

定数は `constexpr` 等で定義できることかと思います。

### キャスト

キャストは C 形式を使わずに, 関数形式、または名前付きキャストにしてください。

```c++
auto i = (int) d; // bad
auto i = int(d);  // good
auto i = static_cast<int>(d); // best
```

### typedef は using にする

積極的に `using` を利用します.

```c++
typedef long long ll; // bad
using ll = long long; // good

typedef int (*f)(double, string);  // bad
using f = int (*)(double, string); // good
```

### range-based for、auto 宣言、構造化束縛などは積極的に用いる

paiza の clang++ は c++17 なのでそこまで利用できるものならば活用しましょう。

```c++
for (const auto& [x, y] : points) { /*...*/ }
```

### auto ... -> ret_type で関数を定義するのは避ける

基本的には全く意味がないので利用しません. ただし `decltype` などを利用するならば後置でよいです.

```c++
int main() { return 0; }         // good
auto main() -> int { return 0; } // bad
```

## 命名

### 省略しすぎない命名をする

基本的に「模範解答」として読みやすい命名をします.

「解答を書く」ことよりも, 「模範解答として読まれる」こと, 「十分に説明的なコードである」ことを強く意識してください.

また, 次のことを意識すると命名の方針が立ちやすいかもしれません.

- その一部を切り抜いたときに自然言語として通用する
- 問題文を読まずともある程度扱っているトピックが分かる

#### bad patterns

- `check`
  - 「素数かどうか」であれば `is_prime`, 「席が空いているか」であれば `seats_available` などの命名をしてください.
- `valid`
  - 「日付として正しいフォーマット」ならば `is_valid_date_format`, もう少し短くてもよい場合は少なくとも `is_valid_format` など一段階具体化してください.
- `count`
  - なんのカウントか不明です.
- `flag`
  - 反転するならば `reverse_flag`, 色を付けるならば `flag_colorize` など書けるはずです.
- `dp`
  - これには強い慣習があると思いますが, `max_values` など書けるならば書くとよいです. 解説にいくらでも DP であることは書けます.

#### 問題文に記載されている「幅 `w`, 高さ `h`」 などの識別子

理想的には `width`, `height` 等の命名をするべきです.

しかし, これは **「問題文という文脈を共有しており, 模範解答の読み手との合意が取れている」** ものとして, 基本的にその文字を変数として利用してよいこととします.

ただし, 下にも説明しますが, `H` や `W` のように「問題文に大文字で指定されている場合」は **「小文字にして」** 利用してください.

```c++
int h, w;          // acceptable
int height, width; // best
int H, W;          // never
```

#### ループ変数 (典型的には `int i`, `some_ptr p` など)

これも可能であれば説明的な命名が良いのですが, **「一般的に広く用いられており, 読み手との合意が得られている」** ものなので, `i` や `p` などの簡易的な命名は許容します.

### 変数および関数は lower_snake_case で命名する

```c++
vector<string> shopping_list; // good
vector<string> shoppingList;  // never

bool content_loaded();        // good
```

また, これは問題解答という側面から出てくる話になりますが, もし **問題文で N, M となっていても**

```c++
int n, m;
cin >> n >> m;
```

のように命名してください.

「`w` の最大値が `W`」などのように大文字小文字で文字が被っているような場合は,

```c++
size_t w_max, w;
```

のように意味を書くことで命名の衝突を避けることが出来るかもしれません.

### クラス、構造体、union は PascalCase で命名する

正直言うと STL/boost に合わせて snake_case の方が収まりが良いのですが, 世の中の慣習としてクラス等は PascalCase で命名する場合がかなり多いです (snake_case を命名の基本としている ruby や rust でもそうです).

これに合わせて, class や struct の命名は `PascalCase` とします.

```c++
class Human {
  // ...
};
```

#### 特例

データ構造の側面が強い構造体・クラスに関しては, `snake_case` での命名を許すこととします. `segment_tree` や `union_find` などが該当します.

```c++
template<typename Monoid>
class segment_tree<Monoid> {
  // ...
};
```

### メンバ

- `private`, `protected`
  - アンダースコアから始まる `_snake_case` とします.
- その他
  - `snake_case` (通常の識別子と同様) とします.

```c++
class some_obj {
private:
  int _how_many_times;
public:
  int total_count;
};
```

### テンプレート型引数

基本的に抽象的な存在であるので, `T`, `S` などを利用します.

ただし, 特にどういうものかを明示したい場合 (モノイドや半群であるなど) に必要ならば `PascalCase` を利用してください.

```c++
template<typename SubGroup>
// ...
```

### 非型テンプレートパラメータは `snake_case`

```c++
template<int seed_value>
int add(int x) {
  return x + seed_value;
}
```

### enum 型名は lower_snake_case / 列挙子は CONSTANT_CASE にする (一旦)

```c++
enum week_days {
  SUNDAY,
  MONDAY,
  TUESDAY,
  WEDNESDAY,
  THURSDAY,
  FRIDAY,
  SATURDAY
};
```

### namespace

`snake_case` としてください.

```c++
namespace some_space {};
```

## 変数

変数の利用に関する規約です.

### グローバル変数は避ける

基本的にグローバル変数は用いないこととします. クラス等にするほうが見通しがよいかもしれません.

#### 例外

`constexpr` なものなどはグローバルで構いません.

```c++
constexpr int mod = 7; // ok
int main() {
  /* ... */
  return 0;
}
```

### 変数は必要な箇所で宣言する

- C++ では C のように関数の先頭で各種変数を宣言するなどの配慮が特に必要ない
- 変数の初期化と宣言が近くなる.
  - その部分だけを切り出して見たときに都合がよい.

```c++
int n, m;
cin >> n >> m;

string s;
cin >> s;

vector<int> v(m);
for (auto i = 0; i < n; i++) {
  int tmp;
  cin >> tmp;
  v[tmp % m]++;
}
```

### 変数のスコープは小さくする

```c++
int i, j;
for (i = 0, j = 0; i + j < n; i++, j += 2) { /* ... */ }
// 以降で i, j を用いていない
```

よりも

```c++
for (int i = 0, j = 0; i + j < n; i++, j += 2) { /* ... */ }
```

のようにかけるならそのようにしてください。

## 関数

<!--
### 関数の引数は 5 個を最大とする

```c++
using point = std::pair<int, int>;
int solve(point start, point goal, point via);
```

多すぎると追うのが大変です。ひとまとまりのものは構造体（こちらを推奨：アクセス時に識別子を分かりやすいものにできるため）や pair などにするとよいかもしれません。
-->

### 関数の引数を書き換える (out 的なパターン) は避ける

このパターンは基本的に避けてください。

基本的には関数の戻り値を利用し、破壊的なものならばクラスのメソッドとして実装するのが丸いと思われます。

```c++
// ちょっと上手いこと書くので待ってね
```

### ラムダ関数式は型を後置で宣言する

## クラス, 構造体

### アクセス修飾子

`private`, `public`, `protected` 等のアクセス修飾子は必ず書いてください.

```c++
class some_class_a {
  bool appreciated; // bad
};

class some_class_b {
private:
  bool appreciated; // good
};
```

## misc

### if や while のブロックの波括弧は毎回書く (推奨)

短く書けるならば短かく書くのがよいのですが, スタイルを合わせるためにこれらは毎回ブロックとして書いてください.

```c++
if (a == b) break; //
if (a == b) {      // good
  break;
}
```

### 桁区切りできるならする (推奨)

```c++
1'000'000'009 // ok
1000000009    // 分かりにくい
```

### 条件式が複雑になる場合は, 一時的に変数を用意する

```c++
if (a == b && (b != c % 4 || d + c / 4 != e) && e * f <= 4) // should avoid

bool some_flag = a == b && (b != c % 4 || d + c / 4 != e) && e * f <= 4; // mmm
if (some_flag)

bool some_flag_what = a == b;
bool some_flag_oops = b != c % 4 || d + c / 4 != e;
bool some_flat_whoa = e * f <= 4;
if (some_flat_what && some_flag_oops && some_flag_whoa) // good
```

### ネストが深くならないように気をつける (早期 return などを使う)

```c++
```

### 真偽値には int ではなく bool を用いる (まあ正直どっちでもいい気もするけど)

```c++
while (1)    // うーん
while (true) // ok
```

### 偶奇判定に &1 をつかわない

剰余をとるという話であれば, すなおに `%` しましょう

```c++
if (i % 2 != 0) // good
if (i & 1)      // ?
```

### データはまとめる (めんどくさくない程度に)

座標を `x`, `y` のようにバラして扱うより, `pair` や `tuple` のように意味のあるかたまりとして纏めることを推奨します.

三次元座標であれば `tuple<int, int, int>` のようにして扱うことができます.
