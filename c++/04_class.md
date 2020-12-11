# 04. クラス

## [許容] `private` アクセス修飾子の省略

`private` アクセス修飾子は書かなくても良いです.

ただし, クラスであればデフォルトで `private`, 構造体であればデフォルトで `public` であることに注意してください.

```c++
class some_class_a {
  bool appreciated; // ok
};

class some_class_b {
private:
  bool appreciated; // ok
};
```
