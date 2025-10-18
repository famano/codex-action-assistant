# Codex Action Assistant

[English](#english) | [日本語](#日本語)

## English

### Overview
This repository provides example GitHub Actions workflows that integrate [openai/codex-action](https://github.com/openai/codex-action) as an issue and pull request assistant. By mentioning `@codex` in issues or pull requests, you can request feedback, ask for code changes, and even let the assistant open a pull request for you.

### Prerequisites
- Add `OPENAI_API_KEY` as a repository or organization secret so the action can authenticate with OpenAI.
- Ensure your project dependencies can be installed without internet access, because Codex runs in an isolated environment.
- Confirm you have permissions to modify workflow files and relevant repository settings.

### Provided Workflows
- `example/codex-issue-assistant.yaml`: Responds to new issues or issue comments that mention `@codex`. It checks out the repository, installs dependencies, creates a branch named `codex/issue-<issue number>-<run id>`, and can optionally open a pull request with Codex's changes.
- `example/codex-pr-assistant.yaml`: Responds to `@codex` mentions on pull requests (comments, review comments, or review bodies). It operates directly on the pull request branch, allowing Codex to make commits and push updates before posting a reply.

### Setup
1. Clone this repository or download the workflow files you need from the `example/` directory.
2. Copy the chosen workflow file(s) into your repository under `.github/workflows/` and rename them if desired.
3. Adjust the dependency setup steps (for example, replace `Set up Node.js` and `npm install`) so they match your project's runtime and tooling.
4. Add the `OPENAI_API_KEY` secret to your repository or organization with a valid OpenAI API key.
5. If you use the Issue Assistant workflow, enable **Allow GitHub Actions to create and approve pull requests** under *Settings > Actions > General > Workflow permissions*.
6. Commit the workflow file(s) and push them to your default branch so the automation is available.

### Usage
- In issues, include `@codex` in the initial body or in a follow-up comment to trigger the Issue Assistant.
- In pull requests, mention `@codex` in a comment, a review comment, or a review body to trigger the PR Assistant.
- Codex checks out your code, follows the guidance baked into each workflow, and replies with feedback. When code changes are needed it commits them with the configured bot identity, pushes the branch, and (for issues) can open a pull request automatically.

### Tips & Limitations
- Codex runs without direct internet access, so make sure all required dependencies are vendored or installable via the provided workflow steps.
- Update the default Node.js version (`24`) and installation commands if your project uses a different language or tooling.
- For the Issue Assistant, Codex creates branches named `codex/issue-<issue number>-<run id>`. If the automatic pull request step fails, you can open one manually from that branch.

## 日本語

### 概要
このリポジトリには、[openai/codex-action](https://github.com/openai/codex-action) をIssueおよびPRのアシスタントとして利用するための GitHub Actions サンプルが含まれています。Issue や PR で `@codex` を呼び出すだけで、フィードバックの取得、コード修正の依頼、必要に応じた PR の作成まで自動化できます。

### 前提条件
- OpenAI への認証に利用する `OPENAI_API_KEY` をリポジトリまたは組織のシークレットとして登録してください。
- Codex は隔離環境で実行されるため、インターネット接続なしで依存関係をインストールできる状態にしておく必要があります。
- ワークフローやリポジトリ設定を変更できる権限を持っていることを確認してください。

### 提供ワークフロー
- `example/codex-issue-assistant.yaml`：`@codex` が含まれる Issue やコメントに反応します。リポジトリをチェックアウトし、依存関係を導入してから `codex/issue-<issue number>-<run id>` という名前のブランチを作成し、必要に応じて Codex が変更を含む PR を自動で作成します。
- `example/codex-pr-assistant.yaml`：PR に対する `@codex` のメンション（コメント、レビューコメント、レビュー本文）に反応します。対象の PR ブランチ上で直接処理を行い、Codex がコミットとプッシュを実行した後に応答を投稿します。

### セットアップ
1. このリポジトリをクローンするか、`example/` ディレクトリから必要なワークフローをダウンロードします。
2. 選択したワークフローを自分のリポジトリの `.github/workflows/` 配下に配置し、必要であればファイル名を変更します。
3. 依存関係の導入手順（例：`Set up Node.js` や `npm install`）を自分のプロジェクトの実行環境に合わせて調整します。
4. 有効な OpenAI API キーを設定した `OPENAI_API_KEY` シークレットをリポジトリまたは組織に追加します。
5. Issue Assistant を利用する場合は、リポジトリの *Settings > Actions > General > Workflow permissions* で **Allow GitHub Actions to create and approve pull requests** を有効にします。
6. ワークフローの変更をコミットしてデフォルトブランチにプッシュし、自動化を有効化します。

### 使い方
- Issue では、本文または追記コメントに `@codex` を含めると Issue Assistant が起動します。
- PR では、コメントやレビューコメント、レビュー本文に `@codex` を含めると PR Assistant が起動します。
- Codex はリポジトリをチェックアウトしてワークフロー内の指示に従い、フィードバックを投稿します。必要に応じて設定済みのボットアカウントでコミットとプッシュを行い、Issue の場合は自動で PR を作成することもできます。

### ヒントと制限事項
- Codex はインターネットにアクセスできない環境で動作するため、必要な依存関係はワークフロー内の手順で導入できるようにしておいてください。
- プロジェクトで別の言語やツールチェーンを使用している場合は、デフォルトの Node.js バージョン（`24`）や `npm install` のコマンドを適切なものに変更してください。
- Issue Assistant は `codex/issue-<issue number>-<run id>` という名前のブランチを作成します。自動 PR 作成に失敗した場合は、そのブランチを使って手動で PR を開いてください。
