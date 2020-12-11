# クラス

## アクセス修飾子

`private`, `public`, `protected` 等のアクセス修飾子は書かなくても良いです.

クラスであればデフォルトで `private`, 構造体であればデフォルトで `public` であることに注意してください.

```c++
class some_class_a {
  bool appreciated; // ok
};

class some_class_b {
private:
  bool appreciated; // ok
};
```
