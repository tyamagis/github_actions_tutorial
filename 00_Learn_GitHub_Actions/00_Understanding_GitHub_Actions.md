# Learn GitHub Actions
（原文）[Understanding GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions?learn=getting_started&learnProduct=actions)

## Understanding GitHub Actions

[1. Overview　概要](https://github.com/tyamagis/github_actions_tutorial/edit/main/00_Learn_GitHub_Actions/Understanding_GitHub_Actions.md#1-overview%E6%A6%82%E8%A6%81)
[2. The components of GitHub Actions　GitHub Actions の構成要素](https://github.com/tyamagis/github_actions_tutorial/edit/main/00_Learn_GitHub_Actions/Understanding_GitHub_Actions.md#2-the-components-of-github-actionsgithub-actions-%E3%81%AE%E6%A7%8B%E6%88%90%E8%A6%81%E7%B4%A0-1)
[3. Create an example workflow　ワークフロー例の作成](https://github.com/tyamagis/github_actions_tutorial/edit/main/00_Learn_GitHub_Actions/Understanding_GitHub_Actions.md#3-create-an-example-workflow%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%95%E3%83%AD%E3%83%BC%E4%BE%8B%E3%81%AE%E4%BD%9C%E6%88%90-1)
[4. Understanding the workflow file　ワークフローのファイルを理解する](https://github.com/tyamagis/github_actions_tutorial/edit/main/00_Learn_GitHub_Actions/Understanding_GitHub_Actions.md#4-understanding-the-workflow-file%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%95%E3%83%AD%E3%83%BC%E3%81%AE%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E7%90%86%E8%A7%A3%E3%81%99%E3%82%8B-1)
[5. Viewing the activity for a workflow run　ワークフロー実行を確認する](https://github.com/tyamagis/github_actions_tutorial/edit/main/00_Learn_GitHub_Actions/Understanding_GitHub_Actions.md#5-viewing-the-activity-for-a-workflow-run%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%95%E3%83%AD%E3%83%BC%E3%81%AE%E5%AE%9F%E8%A1%8C%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B)


## 1. Overview　概要

GitHub Actionsは、ビルド、テスト、デプロイのパイプラインを自動化するための継続的インテグレーションと継続的デリバリー（CI/CD）プラットフォームです。リポジトリへのプルリクエストごとにビルドとテストを行う**ワークフロー**を作成したり、マージされたプルリクエストを本番環境にデプロイしたりすることができます。

<sub>
CI ... Continuous Integration（継続的インテグレーション）, CD ... Continuous Delivery（継続的デリバリー）
</sub>

GitHub Actions は、単なる DevOps にとどまらず、リポジトリで他のイベントが発生したときに**ワークフロー**を実行することができます。例えば、誰かがリポジトリに新しい課題を作成すると、自動的に適切なラベルを追加する**ワークフロー**を実行することができます。

GitHub は、**ワークフロー**を実行するための Linux、Windows、macOS の仮想マシンを提供します。また、独自のデータセンターやクラウドインフラでセルフホスティングの**ランナー**をホストすることも可能です。


## 2. The components of GitHub Actions　GitHub Actions の構成要素

GitHub Actions の**ワークフロー**は、プルリクエストがオープンされたときや issue が作成されたときなど、リポジトリで**イベント**が発生したときに起動するように設定することができます。**ワークフロー**には一つまたは複数の**ジョブ**が含まれ、順次、または並行して実行されます。各**ジョブ**は、独自の仮想マシンの**ランナー**内、またはコンテナ内で実行され、定義したスクリプトを実行するか、**ワークフロー**を簡素化する再利用可能な拡張機能である** action **を実行する 1 つまたは複数のステップを持っています。

![](https://docs.github.com/assets/cb-25535/images/help/images/overview-actions-simple.png)

#### 2-1. Workflow ワークフロー

**ワークフロー**は、1 つまたは複数の**ジョブ**を実行する設定可能な自動化プロセスです。ワークフローは、リポジトリにチェックインされた YAML ファイルによって定義され、リポジトリ内の**イベント**によってトリガーされたときに実行されるか、手動でトリガーされるか、定義されたスケジュールで実行されます。

ワークフローはリポジトリの `.github/workflows` ディレクトリで定義され、リポジトリは複数のワークフローを持つことができ、それぞれが異なるタスクセットを実行することができます。例えば、プルリクエストをビルドしてテストするワークフロー、リリースが作成されるたびにアプリケーションをデプロイするワークフロー、誰かが新しい課題をオープンするたびにラベルを追加するワークフローなどがあります。

ワークフローは、他のワークフローから参照することができます。参照：[Reusing workflows - GitHub Docs](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

ワークフローの詳細については、[Using workflows - GitHub Docs](https://docs.github.com/en/actions/using-workflows)を参照してください。


#### 2-2. Events イベント

**イベント**とは、**ワークフロー**を実行するきっかけとなる、リポジトリ内の特定の活動のことです。たとえば、誰かがプルリクエストを作成したり、課題を開いたり、リポジトリにコミットをプッシュしたりすると、GitHub からアクティビティが発生することがあります。また、スケジュールや REST API への投稿、手動でワークフローの実行をトリガーすることもできます。

ワークフローのトリガーとなるイベントの一覧は、[Events that trigger workflows - GitHub Docs](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)を参照ください。

#### 2-3. Jobs ジョブ

**ジョブ**は、同じ**ランナー**で実行される**ワークフロー**内のステップのセットです。各ステップは、実行されるシェルスクリプト、または実行される**アクション**のいずれかです。ステップは順番に実行され、互いに依存し合っています。各ステップは同じランナー上で実行されるので、あるステップから別のステップへデータを共有することができます。例えば、アプリケーションをビルドするステップと、ビルドしたアプリケーションをテストするステップを用意することができます。

ジョブは他のジョブとの依存関係を設定できます。デフォルトでは、ジョブは依存関係を持たず、互いに並行して実行されます。あるジョブが他のジョブに依存する場合、そのジョブは依存するジョブの完了を待って実行されます。たとえば、依存関係のない異なるアーキテクチャの複数のビルドジョブと、それらのジョブに依存するパッケージングジョブがあるとします。ビルドジョブは並行して実行され、それらがすべて正常に完了すると、パッケージングジョブが実行されます。

ジョブの詳細については、"ジョブの使用 "を参照してください。

#### 2-4. Actions アクション

アクションは、GitHub Actions プラットフォームのカスタムアプリケーションで、複雑だけど頻繁に繰り返されるタスクを実行します。アクションを使えば、ワークフローファイルで繰り返し書くコードの量を減らすことができます。アクションは、GitHub から git リポジトリを取得したり、ビルド環境に適したツールチェインを設定したり、クラウドプロバイダーへの認証を設定したりできます。

自分でアクションを作成することもできますし、GitHub Marketplace でワークフローで使用するアクションを見つけることもできます。

詳しくは、"アクションの作成" をご覧ください。

#### 2-5. Runnnes ランナー

ランナーとは、ワークフローがトリガーされたときに実行するサーバーのことです。各ランナーは、一度に一つのジョブを実行することができます。GitHub は、ワークフローを実行するための Ubuntu Linux、Microsoft Windows、macOS ランナーを提供しています。各ワークフローの実行は、新しくプロビジョニングされた仮想マシンで行われます。別のオペレーティングシステムが必要な場合や、特定のハードウェア構成が必要な場合は、独自のランナーをホストすることができます。自前ランナーの詳細については、"自前ランナーのホスティング "を参照してください。

## 3. Create an example workflow　ワークフロー例の作成

GitHub Actions は、ワークフローの定義に YAML 構文を使用します。各ワークフローは、コードリポジトリの `.github/workflows` というディレクトリに個別の YAML ファイルとして保存されます。

リポジトリにワークフローの例を作成すると、コードがプッシュされるたびに一連のコマンドを自動的にトリガーすることができます。このワークフローでは、GitHub Actions がプッシュされたコードをチェックアウトし、[bats - npm](https://www.npmjs.com/package/bats) テストフレームワークをインストールし、bats のバージョンを出力する基本コマンド`bats -v.`を実行します。

手順 1. リポジトリに、ワークフローファイルを格納するための`.github/workflows/`ディレクトリを作成します。

手順 2. `.github/workflows/` ディレクトリに、`learn-github-actions.yml`というファイルを新規作成し、以下のコードを追加してください。

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```

3-3. これらの変更をコミットして GitHub リポジトリにプッシュします。

これで GitHub Actions のワークフローファイルがリポジトリにインストールされ、誰かがリポジトリに変更をプッシュするたびに自動的に実行されるようになりました。ワークフローの実行履歴の詳細を見るには、"Viewing the activity for a workflow run" を参照ください。

www.DeepL.com/Translator（無料版）で翻訳しました。

## 4. Understanding the workflow file　ワークフローのファイルを理解する

```yaml
name: learn-github-actions
```
オプション - GitHub リポジトリの Actions タブに表示されるワークフローの名前です。

```yaml
on: [push]
```
このワークフローのトリガーを指定します。この例では push イベントを使用しています。誰かがリポジトリに変更をプッシュしたりプルリクエストをマージしたりするたびに、ワークフローの実行がトリガーされることになります。これは、すべてのブランチへのプッシュがトリガーとなります。特定のブランチやパス、タグへのプッシュのときだけ実行する構文の例については、"GitHub Actions のワークフロー構文" を参照ください。

```yaml
jobs:
```
learn-github-actions ワークフローで実行されるすべてのジョブをグループ化します。

```yaml
  check-bats-version:
```
check-bats-version という名前のジョブを定義します。子キーでジョブのプロパティを定義します。

```yaml
    runs-on: ubuntu-latest
```
最新版のUbuntu Linuxランナーで実行されるようにジョブを設定します。これは、GitHub がホストする新しい仮想マシン上でジョブが実行されることを意味します。他のランナーを使った構文の例については、"GitHub Actions のワークフロー構文" を参照してください。

```yaml
    steps:
```
check-bats-version ジョブで実行されるすべてのステップをグループ化します。このセクションの下にネストされた各項目は、個別のアクションまたはシェルスクリプトです。

```yaml
      - uses: actions/checkout@v3
```
uses キーワードは、このステップが actions/checkout アクションの v3 を実行することを指定します。これは、リポジトリをランナー上にチェックアウトするアクションで、コードに対してスクリプトや他のアクション（ビルドツールやテストツールなど）を実行できるようにするものです。ワークフローがリポジトリのコードに対して実行される場合は、常に checkout アクションを使用する必要があります。

```yaml
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
```
このステップでは、actions/setup-node@v3 アクションを使用して、指定されたバージョンの Node.js をインストールします（この例では v14 を使用します）。これにより、PATH に node と npm コマンドの両方が置かれます。

```yaml
      - run: npm install -g bats
```
runキーワードは、ランナー上でコマンドを実行するようジョブに指示します。この場合、npmを使ってbatsソフトウェアテストパッケージをインストールします。

```yaml
      - run: bats -v
```
最後に、ソフトウェアのバージョンを出力するパラメータを指定して、batsコマンドを実行します。

#### 4-1. Visualizing the workflow file ワークフローファイルを可視化する

この図では、先ほど作成したワークフローファイルと GitHub Actions のコンポーネントがどのように階層化されているのかを確認できます。各ステップは、ひとつのアクションあるいはシェルスクリプトを実行します。ステップ 1 と 2 はアクションを実行し、ステップ 3 と 4 はシェルスクリプトを実行します。ワークフローに必要な既成のアクションをもっと探すには、"Finding and customizing actions" を参照ください。

![visualizing_the_workflow_file](https://docs.github.com/assets/cb-33882/images/help/images/overview-actions-event.png)

## 5. Viewing the activity for a workflow run　ワークフローの実行を確認する

ワークフローがトリガーされると、ワークフローを実行する`workflow run`が作成されます。`wworkflow run`が開始されると、実行の進捗を視覚化したグラフが表示され、各ステップのアクティビティを GitHub で確認することができます。

手順 1. GitHub.comで、リポジトリのメインページに移動します。

手順 2. リポジトリ名の下にある、Actions をクリックします。

手順 3. 左側のサイドバーで、確認したいワークフローをクリックします。

手順 4. Workflow runs "の下にある、確認したい`workflow run`の名前をクリックします。

手順 5. Jobsまたは可視化グラフで、確認したいジョブをクリックします。

手順 6. 各ステップの結果を表示します。
