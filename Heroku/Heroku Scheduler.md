# Heroku Scheduler

## create heroku app

1. login

    何かしらのキーを押すとブラウザが立ち上るのでログインする。

    ``` bash
    heroku login
    ```

2. create heroku app

    Herokuにアプリケーションを作成します。

    ``` bash
    heroku create $HEROKU_APP_NAME
    ```

## deploy

1. Regist Heroku remote repository

    リモートリポジトリにHerokuを登録する。

    ``` bash
    heroku git:remote -a $HEROKU_APP_NAME
    ```

2. show remote repository

    リモートリポジトリを確認する。

    ``` bash
    git remote -v
    ```

3. push origin

    originへpushする。
    この作業は行わなくてもHerokuへのデプロイは行えるがリリースブランチにpushしたのちデプロイするのが望ましい。

    ``` bash
    git push origin $BRANCH_NAME
    ```

4. deploy heroku

    Herokuへデプロイする。
    自動でビルドが実行されエラーがなければデプロイされる。

    ``` bash
    git push heroku $BRANCH_NAME
    ```

## setting Heroku Scheduler

1. add Heroku Scheduler

    Heroku Schedulerの追加を行う。

    ``` bash
    heroku addons:create scheduler:standard
    ```

2. open Heroku Scheduler

    Heroku Schedulerの設定はCLIでは行えないため、ブラウザ上の設定画面を開く。

    ``` bash
    heroku addons:open scheduler
    ```

3. create job

    - ジョブを作成する。
    - 任意の実行タイミングを設定する。
      - UTCでの設定なので、設定したいJSTから-9:00で設定する。
    - 任意の実行コマンドを設定する。
      - アプリケーションを実行したい場合は、

        ``` bash
        heroku run ./bin/$HEROKU_APP_NAME
        ```
