# Azure DevOps

Azure DevOps とはプロジェクト管理ツール群が集約されたサービスでDevOps (開発と運用が連携する)の考え方に基づいている。
主にタスク管理、ソース管理、テスト・デプロイ等の自動化を行うことができる。

## Bords

各種タスクを管理する。Basic、Agaile 等のプロセスがありプロジェクトごとにプロセスを設定することが可能。
基本的にアジャイル思想に基づいて作られたサービスのためAgaile のプロセスを選択するのが吉。

### Sprintの設定方法

1. Project Setting からTeamsを作成する。
2. Project Setting -> Project Configration から各イテレーションを作成する。
3. Boards -> Sprints -> NewSprint から Select existing iteration を選択し2.で作成したイテレーションと紐づけを行う。
4. WorkItemを各スプリントに配置する。

## Artifacts

Azure Artifactsは、パッケージのためのリポジトリサービスとして機能するAzure DevOpsのラインナップのひとつです。
共通処理等をCommonパッケージとして切り出し全てのプロジェクトから呼び出す等の使い方が可能。

## PAT

Parsonal Access Token（PAT）は、AzureDevOpsへの認証の代替パスワードとして使用されます。
Azure DevOpsの右上のUserSttringで発行でき、各種権限の設定や有効期限の設定も可能です。
