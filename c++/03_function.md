# 03. 関数

## [推奨] 関数の引数は少なくする

データをまとめるということにも関連してきます. たとえば, 二次元座標を扱う場合には `std::pair<int, int>` などにしてしまうほうが読みやすいでしょう.

```c++
// not good
path traverse(int start_x, int start_y, int goal_x, int goal_y, int via_x, int via_y) {
  /* ... */
}

// better
path traverse(point start, point goal, point via) {
  /* ... */
}
```

<!--
## [回避] 関数の引数を書き換える (out 的なパターン) は避ける

このパターンは基本的に避けてください。

基本的には関数の戻り値を利用し、破壊的なものならばクラスのメソッドとして実装するのが丸いと思われます。

```c++
// ちょっと上手いこと書くので待ってね
```
-->
