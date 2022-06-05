# reference
GitHub Actions Documentation - GitHub Docs (https://docs.github.com/en/actions)

## Creating your first workflow [JP]
1. `.github/workflows` ディレクトリをレポジトリ内に作成
2. `github-actions-demo.yml` を `.github/workflows` ディレクトリ内に作成
3. `github-actions-demo.yml` に以下の内容を記述

```YAML
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
