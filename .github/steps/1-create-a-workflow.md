## Step 1: ワークフローファイルの作成

_Welcome to "Hello GitHub Actions"! :wave:_

**_GitHub Actions_ とは？**: GitHub Actions は、チームのソフトウェアワークフローのほぼすべての側面を自動化する柔軟な方法を提供します。テストの自動化、継続的なデプロイ、コードのレビュー、問題の管理やプルリクエストなどを行うことができます。最も良い点は、これらのワークフローはコードとしてリポジトリに保存され、チーム間で簡単に共有して再利用できることです。詳細については、次のリソースを確認してください :

- GitHub Actions の機能についてはこちらを参照ください [GitHub Actions](https://github.com/features/actions)
- "GitHub Actions" ドキュメントはこちらを参照ください [GitHub Actions](https://docs.github.com/actions)

**_workflow_ とは？**: ワークフローとは、1つ以上のジョブを実行する構成可能な自動プロセスです。ワークフローは `.github/workflows` ディレクトリ内の特別なファイルで定義され、選択したイベントに基づいて実行されます。この演習では、`pull_request` イベントを使用します。

- ワークフロー、ジョブ、イベントについてはこちらをご確認ください : "[Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)"
- `pull_request` イベントについて使用前に詳しく知りたい場合は、こちらをご確認ください : "[pull_request](https://docs.github.com/en/developers/webhooks-and-events/webhooks/webhook-events-and-payloads#pull_request)".

演習を始めるため、新しいリポジトリでアクションワークフローを実行し、`welcome-workflow`という作業用のブランチを作成していきます。

### :keyboard: Activity: ワークフローファイルを作成する

1. ブラウザで新しいタブを開き、同じリポジトリに移動します。次に、このタブの手順を読みながら、2 番目のタブの手順に取り組みます
1. プルリクエストを作成します。これには、コースのこの部分で行うすべての変更が含まれます

   **Pull Requests** タブをクリックし、**New pull request** をクリックして、`base: main`と`compare:welcome-workflow`を設定し、**Create pull request** をクリックして、再び**Create pull request**をクリックします。

1. **Code**タブに移動する
1. **main** ブランチをクリックしドロップダウンリストから **welcome-workflow** ブランチを選択する
1. `.github/workflows/` フォルダーに移動し、**Add file** を選択、**Create new file**をクリックする
1. **Name your file** フィールドには`welcome.yml`と入力する
1. `welcome.yml`ファイルに次の内容を記述する :

   ```yaml copy
   name: Welcome コメントの投稿
   on:
     pull_request:
       types: [opened]
   permissions:
     pull-requests: write
   ```

1. 変更をコミットするために、**Commit changes**をクリックする
1. コミットメッセージを入れ、**Commit directly to the welcome-workflow branch**を選択し、**Commit changes**をクリックする
1. 約 20 秒待ってから、このページ (指示に従っているページ) を更新します。リポジトリ内の (作成したワークフローではない) 別のアクションワークフローが実行され、この README ファイルの内容が次の手順の手順に自動的に置き換えられます
