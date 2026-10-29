# Dependabot Auto Merge for YassLab team

YassLab チーム用の Dependabot カスタムアクションです。

[&raquo; デフォルト設定を見る](https://github.com/yasslab/dependabot_auto_merge/blob/main/action.yml)   
[&raquo; レビュー利用例を見る](https://github.com/yasslab/yasslab.jp/blob/main/.github/workflows/dependabot.yml)   
[&raquo; 関連リポジトリを見る](https://github.com/yasslab/claude_review_action)

<br>



## Example Usage

```bash
.github/workflows/dependabot.yml
```

```yaml
name: Auto-merge Dependabot PRs
on:
  pull_request:
  # Allows you to run this workflow manually from the Actions tab
  # https://docs.github.com/en/actions/managing-workflow-runs/manually-running-a-workflow
  workflow_dispatch:

permissions:
  contents:      write
  pull-requests: write
  checks:        read # CI の結果を読む（private リポジトリで必要）
  statuses:      read # 同上

jobs:
  dependabot:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]'
    steps:
      - uses: yasslab/dependabot_auto_merge@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

### 必要な設定

- Settings → General → "Allow auto-merge" を有効化
- Settings → Actions → General → Workflow permissions → "Allow GitHub Actions to create and approve pull requests" を有効化（無いと PR の承認で止まる）
- workflow の `permissions` に `checks: read` と `statuses: read` を書く（`wait-for-ci: true` の時に CI の結果を読む。private リポジトリでは無いと `Resource not accessible by integration` で止まる）

### 使用できるオプション

|     パラメータ      |   デフォルト   |     説明     |
|---------------------|----------------|--------------|
| `merge-level`       | `all`          | 自動マージする最大レベル (`patch`, `minor`, `all`) |
| `merge-method`      | `squash`       | マージ方法 (`merge`, `squash`, `rebase`) |
| `exclude-gems`      | `rails,jekyll` | 除外するRuby gem（カンマ区切り）         |
| `wait-for-ci`       | `true`         | CIが通るまで待機してマージ（最大60分）   |

-----

Copyright © [YassLab](https://github.com/yasslab).
