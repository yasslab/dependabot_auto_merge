# Dependabot Auto Merge for YassLab team

YassLab チーム用の Dependabot カスタムアクションです。

[» デフォルト設定を見る](https://github.com/yasslab/dependabot_auto_merge/blob/main/dependabot.yml)

## Example Usage

```bash
.github/workflows/dependabot.yml
```

```yaml
name: Auto-merge Dependabot PRs
on: pull_request

permissions:
  contents: write
  pull-requests: write

jobs:
  dependabot:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]'
    steps:
      - uses: yasslab/dependabot_auto_merge@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

これでpatchとminorアップデートが自動的にマージされます。

### 必要な設定

リポジトリの Settings → General → "Allow auto-merge" を有効化

### 使用できるオプション

|     パラメータ      | デフォルト |     説明     |
|---------------------|------------|--------------|
| `auto-merge-level`  | `minor`    | 自動マージする最大レベル (`patch`, `minor`, `all`) |
| `merge-method`      | `squash`   | マージ方法 (`merge`, `squash`, `rebase`) |
| `exclude-packages`  | なし       | 除外するパッケージ（カンマ区切り） |
| `dry-run`           | `false`    | テスト実行（実際にはマージしない） |
| `wait-for-checks`   | `false`    | CIが通るまで待機してマージ（最大60分） |

-----

Copyright © [YassLab](https://github.com/yasslab).
