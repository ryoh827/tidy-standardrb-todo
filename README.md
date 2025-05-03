# StandardRB Fix One File Action

このアクションは、指定した数だけ `.standard_todo.yml` の ignore リストからファイルを選び、`standardrb --fix` を実行します。

## 入力パラメータ
- `todo_file` (任意): standard_todo.ymlのパス（デフォルト: `.standard_todo.yml`）
- `fix_count` (任意): 修正するファイル数（デフォルト: 1）

## 使い方（ワークフロー例）

```yaml
jobs:
  standardrb-fix:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Ryoh827/auto-standardrb-pr@v1
        with:
          todo_file: '.standard_todo.yml'   # 省略可
          fix_count: 2                      # 例: 2ファイル修正
```

> ※ `standardrb` のインストールや `Gemfile` の用意は、リポジトリ側で事前に行ってください。
