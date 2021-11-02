## 全体的なルール

#### 対象講座: 新・アルゴリズムとデータ構造入門Java編, etc...

```
import java.util.*;  // import文の展開の是非は自由

public class Main {  // '{'の手前には半角スペースをいれる
    public static void main(String[] args) { // 引数の配列・多倍長(...)の選択は自由
        int n = 5;
        for (int i = 0; i < n; i++) {  // forやifと'('の間にはスペース
            System.out.println("Hello World");
        }
        // 変数名はパスカルケース、クラス名はキャメルケース
        int sumOfCookies = 1 << 20; // 代入演算子やその他の二項演算子の後ろには意味のまとまりなど気にせずスペースをいれる
    }
    // 半角スペース4つでインデント
}
```

## 個別のルール

#### 対象講座: 新・Java入門編

- メインメソッドは多倍長引数にする
```
    public static void main(String... args) {
    }
```
