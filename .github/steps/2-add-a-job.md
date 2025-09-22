## Step 2: ワークフローファイルにジョブを追加する

_よくできました! :tada: workflow fileの追加に成功しました!_

`welcome-workflow`ブランチの`welcome.yml`ファイル内のエントリの意味は次のとおりです :

- `name: Welcome コメントの投稿` ワークフローに名前を付けます。この名前は、リポジトリのアクションタブに表示されます 
- `on: pull_request: types: [opened]` 誰かがプルリクエストを[開く]たびにワークフローが実行されることを示しています
- `permissions` リポジトリ上で操作のためのワークフローの権限を割り当てます
- `pull-requests: write` プルリクエストへの書き込み権限を付与しています（これはWelcomeコメントを作成するために必要です）

続いて、実行するジョブを指定する必要があります

**_job_ とは？**: ジョブは、同じランナー(トリガーされたときにワークフローを実行するサーバー)上で実行されるワークフロー内の一連のステップです。トリガー(例:誰かがプルリクエストを[開く])されたワークフローはランナー上で動き、そのワークフローにはジョブがあり、ジョブにはステップがあります。ステップは順番に実行され、相互依存しています。この演習の後半でワークフローにステップを追加します。ジョブの詳細については、「[Jobs](https://docs.github.com/en/actions/learn-github-actions/Understanding-github-actions#jobs)」を参照してください。

次のアクティビティでは、作成したワークフローに"build"ジョブを追加します。利用可能で高速でコストの安い `ubuntu-latest`ジョブランナーを指定します。なぜこのランナーを利用するのかについて詳しく知りたい方は、こちらの記事"[Understanding the workflow file](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#understanding-the-workflow-file)"の中の`runs-on: ubuntu-latest`の部分に説明されていますのでご確認ください。

### :keyboard: Activity: ワークフローファイルにジョブを追加する

1. ブラウザの別タブで`welcome-workflow`ブランチにいることを確認し、`.github/workflows/welcome.yml`ファイルを開く
1. ファイルの中身を以下のように更新する :

   ```yaml copy
   name: Post welcome comment
   on:
     pull_request:
       types: [opened]
   permissions:
     pull-requests: write
   jobs:
     build:
       name: Post welcome comment
       runs-on: ubuntu-latest
   ```

1. ワークフローエディタの右上にある**Commit changes**をクリックする
1. コミットメッセージを書き、`welcome-workflow`ブランチに対して直接コミットする
1. 約20秒待ってからこのページ (指示に従っているページ) を更新する。別のワークフローが実行され、この README ファイルの内容が次のステップの手順に置き換えられます
