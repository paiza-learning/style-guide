# PHP 模範解答コーディングルール

## 概要
PSR-1, PSR-2 と Symfony のコーディングルールを基に作成。

## コード例
あとで書く

## テスト方法(仮)
[FriendsOfPHP/PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) を使用して自動フォーマットが行える。

### 前提
```zsh
~ ❯ cd ~/paiza

~/paiza ❯ tree -L 1
.
├── learning_problem
└── style-guide

2 directories, 0 files
```

### php-cs-fixer インストール
```zsh
~ ❯ brew install php-cs-fixer
```
PHP8.0では動かないので、適当なバージョンに切り替える。
```zsh
~ ❯ brew install php@7.4
~ ❯ brew unlink php
~ ❯ brew link php@7.4
```

### フォーマット実行
```zsh
~/paiza/learning_problem ❯ php-cs-fixer fix --config ~/paiza/style-guide/php/.php_cs.dist --diff --diff-format udiff **/*.php
```

