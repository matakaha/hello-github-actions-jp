## Step 3: ワークフローファイルにステップを追加する

_ワークフローにジョブを追加することができましたね！ 素晴らしい！ :dancer:_

ワークフローにはジョブが入っていて、ジョブにはステップが入っています。ここではワークフローにステップを追加してみましょう

**_steps_ とは？**: アクションステップは、ワークフローのジョブが実行されるときに上から下へ１つ１つ順番に実行されます。各々のステップをきちんとパスしなければ次のステップには進みません。

各ステップは、実行されるシェルスクリプトか、実行されるアクション（action）への参照のいずれかで構成されます。この文脈で「action（小文字）」と言う場合は、再利用可能なコード単位を指します。アクションについては「[Finding and customizing actions](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions)」で知ることができますが、ここではワークフローステップでシェルスクリプトを使います。

ワークフローを更新して、新しいプルリクエストが作成されたときにコメントを投稿するようにしましょう。これは [bash](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) スクリプトと [GitHub CLI](https://cli.github.com/) を使って実現します。

### :keyboard: Activity: ワークフローファイルにステップを追加しよう

1. まだ `welcome-workflow` ブランチで作業中の状態で、`welcome.yml` ファイルを開く
1. ファイルの内容を以下のように更新する

   ```yaml copy
   name: Welcome コメントの投稿
   on:
     pull_request:
       types: [opened]
   permissions:
     pull-requests: write
   jobs:
     build:
       name: Post welcome comment
       runs-on: ubuntu-latest
       steps:
         - run: gh pr comment $PR_URL --body "Welcome to the repository!リポジトリへようこそ！"
           env:
             GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
             PR_URL: ${{ github.event.pull_request.html_url }}
   ```

   **Note:** 追加したステップは、プルリクエストが作成されたときに GitHub CLI (`gh`) を使ってコメントを追加します。GitHub CLI がコメントを投稿できるようにするために、`GITHUB_TOKEN` 環境変数を `GITHUB_TOKEN` シークレットの値に設定します。これは、ワークフローが実行されるときに作成されるインストールアクセストークンです。詳細については、「[Automatic token authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)」を参照してください。`PR_URL` 環境変数には、新しく作成されたプルリクエストの URL を設定し、`gh` コマンドで使用します。

1. ワークフローエディタの右上にある **Commit changes** をクリックする
1. コミットメッセージを入力し、変更を直接ブランチにコミットする
1. 約 20 秒待ってから、このページを更新する（指示に従っているページ）。別のワークフローが実行され、この README ファイルの内容が次のステップの指示に置き換えられます。
