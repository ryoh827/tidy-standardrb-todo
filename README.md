# StandardRB Fix One File Action

このアクションは、指定した数だけ `.standard_todo.yml` の ignore リストからファイルを選び、`standardrb --fix` を実行します。

## standard-ruby-actionとの違い

- `standard-ruby-action`はリポジトリ全体に対して`standardrb --fix`を実行しますが、このアクションは`.standard_todo.yml`のignoreリストから指定した数のファイルのみを修正します
- このアクションは、大きなプロジェクトで段階的にコードを修正していく場合に特に有用です
- 修正対象のファイルを制御できるため、CIの実行時間を短縮できます

## 入力パラメータ
- `fix_count` (任意): 修正するファイル数（デフォルト: 1）

## 使い方（ワークフロー例）

```yaml
jobs:
  standardrb-fix:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.4'
      - uses: Ryoh827/auto-standardrb-pr@v1
        with:
          fix_count: 2                      # 例: 2ファイル修正
      - name: update .standard_todo.yml
        run: |
          bundle exec standardrb --generate-todo || true
      - name: Verify .standard_todo.yml is empty
        run: |
          if [ "$(yq '.ignore | length' .standard_todo.yml)" != "0" ]; then
            echo "Error: .standard_todo.yml has unexpected content"
            cat .standard_todo.yml
            exit 1
          fi
```

> ※ `standardrb` のインストールや `Gemfile` の用意は、リポジトリ側で事前に行ってください。
