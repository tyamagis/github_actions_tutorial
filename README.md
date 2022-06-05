# reference
[ GitHub Actions Documentation - GitHub Docs ](https://docs.github.com/en/actions)

for me and jp-lang reader.

## 処理を作成
1. `.github/workflows` ディレクトリをレポジトリ内に作成
2. `github-actions-demo.yml` を `.github/workflows` ディレクトリ内に作成
3. `github-actions-demo.yml` に以下の内容を記述

```yaml{:copy}
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v3
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```
4. **Create a new branch for this commit and start a pull request** -> **Propose new file** をすることで push イベントが走り、YAML ファイルに記述した処理が実行される。

## 処理結果を見る

1. レポジトリ上部の Actions タブに移動
2. 作成した処理（Jobs）を選択
3. `Explore-GitHub-Actions` を選択
4. 処理が表示されるので詳細を確認したい処理を選んで確認
