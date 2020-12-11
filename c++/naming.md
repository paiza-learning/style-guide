# 命名

## 省略しすぎない命名をする

基本的に「模範解答」として読みやすい命名をします.

「解答を書く」ことよりも, 「模範解答として読まれる」こと, 「十分に説明的なコードである」ことを強く意識してください.

また, 次のことを意識すると命名の方針が立ちやすいかもしれません.

- その一部を切り抜いたときに自然言語として通用する
- 問題文を読まずともある程度扱っているトピックが分かる

### bad patterns

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

### 問題文に記載されている「幅 `w`, 高さ `h`」 などの識別子

理想的には `width`, `height` 等の命名をするべきです.

しかし, これは **「問題文という文脈を共有しており, 模範解答の読み手との合意が取れている」** ものとして, 基本的にその文字を変数として利用してよいこととします.

ただし, 下にも説明しますが, `H` や `W` のように「問題文に大文字で指定されている場合」は **「小文字にして」** 利用してください.

```c++
int h, w;          // acceptable
int height, width; // best
int H, W;          // never
```

### ループ変数 (典型的には `int i`, `some_ptr p` など)

これも可能であれば説明的な命名が良いのですが, **「一般的に広く用いられており, 読み手との合意が得られている」** ものなので, `i` や `p` などの簡易的な命名は許容します.

## 変数および関数は lower_snake_case で命名する

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

## クラス、構造体、union は PascalCase で命名する

正直言うと STL/boost に合わせて snake_case の方が収まりが良いのですが, 世の中の慣習としてクラス等は PascalCase で命名する場合がかなり多いです (snake_case を命名の基本としている ruby や rust でもそうです).

これに合わせて, class や struct の命名は `PascalCase` とします.

```c++
class Human {
  // ...
};
```

### 特例

データ構造の側面が強い構造体・クラスに関しては, `snake_case` での命名を許すこととします. `segment_tree` や `union_find` などが該当します.

```c++
template<typename Monoid>
class segment_tree<Monoid> {
  // ...
};
```

## メンバ

- `private`, `protected`
  - アンダースコアから始まる `_snake_case` とします.
- その他
  - `snake_case` (通常の識別子と同様) とします.

```c++
class some_obj {
  int _how_many_times;
public:
  int total_count;
};
```

## テンプレート型引数

基本的に抽象的な存在であるので, `T`, `S` などを利用します.

ただし, 特にどういうものかを明示したい場合 (モノイドや半群であるなど) に必要ならば `PascalCase` を利用してください.

```c++
template<typename SubGroup>
// ...
```

## 非型テンプレートパラメータは `snake_case`

```c++
template<int seed_value>
int add(int x) {
  return x + seed_value;
}
```

## enum 型名は lower_snake_case / 列挙子は CONSTANT_CASE にする

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

## namespace

`snake_case` としてください.

```c++
namespace some_space {};
```
