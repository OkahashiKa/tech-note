# docker-composeでローカルDBを爆速で構築する

## はじめに

この記事は「[PERSOL PROCESS & TECHNOLOGY Advent Calendar 2021](https://qiita.com/advent-calendar/2021/ppt)」の18日目の記事です。
興味がある方はぜひ他の記事もご覧ください。

こんにちわ。猫を飼い始めたことで家から出る機会が本当に減り、お腹に脂肪を爆速で構築している人です。
当方脳を猫と脂肪に侵食されておりますので、内容がでたらめな場合はご指摘のほどよろしくお願いいたします。

本日は、脂肪を爆速で構築する方法ではなく、個人開発やちょっとした検証の際に私がよく使っている、dockerを用いたローカルDBの構築を記事にしたいと思います。

今回はサンプルとしてPostgreSQLで構築します。

## PostgreSQLコンテナを作成

まずは、ターミナルを起動しておもむろに以下のコマンドを叩きます。

``` Bash
docker run -d --name sample-db -p 65432:5432 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=passwd -e POSTGRES_DB=sample-db postgres:13
```

完了です。dockerのインストールから始めても5秒でできますね！

DBクライアント等、思い思いの方法で接続してみてください。
postgresqlをインストールしている人は以下のコマンドで接続してみてください。
ちゃんとDBに接続できるはずです。

``` Bash
psql -h localhost -p 65432 -U postgres -d sample-db
```

あとはテストデータを作って検証するなど好きに使い倒してください。
気が済んだら以下のコマンドでコンテナを削除できます。

``` Bash
# コンテナの停止
docker stop sample-db

# コンテナの削除
docker rm sample-db
```

ローカルにPostgreSQLコンテナは構築できましたが、流石にこれだけでは芸がないので他にもいろいろ試してみましょう。

## docker-composeでPostgreSQLコンテナを作成

上で作ったPostgreSQLコンテナと同等のコンテナをdocker-composeで構築してみます。
まずは、任意のディレクトリにdocker-compose.yamlを作成します。

``` yaml
version: '3'
services:
  postgresql:
    image: postgres:13
    container_name: sample-db
    ports:
      - 65433:5432
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: passwd
      POSTGRES_DB: sample-db
```

次に以下のコマンド実行しコンテナを起動します。

``` Bash
docker compose up -d
```

完了です。
こちらも簡単ですね。所要時間はざっと8秒といったところでしょうか。

ひとしきり検証を終えたら以下のコマンドでコンテナを削除できます。

``` bash
docker compose down
```

## 初期データの挿入とDBの複製

手元に検証用DBを作りたい場合の中には、本番DBや開発用DBなど何かしらの元となるDBが存在し、その複製を作りたいという場合も往々にして存在するかと思います。
その場合は、上のPostgreSQLコンテナを起動する際に初期データをしてdumpを流し込むshを呼び出すことで実現可能です。

最終的なフォルダ構成としては以下のようになります。

``` test
docker-compose.yaml
initdb.d
┗init-sample-db.sh
┗sample-db.ddl
┗sample-db.dml
```

1. dumpの取得

    まずは、複製元のDBのdumpを取ります。

    ``` bash
    # schema only
    pg_dump -h $HOST_NAME -p $PORT --schema-only $DATABASE_NAME > sample-db.ddl

    # deta only
    pg_dump -h $HOST_NAME -p $PORT --data-only $DATABASE_NAME > sample-db.dml
    ```

    取得したdumpをinitdb.dディレクトリに格納します。
    （本番DBのデータを取ってきた際は必ず個人情報等のデータは必ずマスキングしましょう。）

2. 初期データ挿入shの作成

    ``` sh
    #!/bin/bash
    set -e

    psql -d ${POSTGRES_DB} -f /docker-entrypoint-initdb.d/sample-db.ddl
    psql -d ${POSTGRES_DB} -f /docker-entrypoint-initdb.d/sample-db.dml
    ```

    作成したshをinitdb.dディレクトリに格納します。

3. docker-composeの編集

    先ほど作成したdocker-compose.yamlに初期データ挿入shをマウントする設定を追記します。
    「/docker-entrypoint-initdb.d」にマウントしたディレクトリに「.sql」「.sh」等の拡張子でファイルを配置しておくと、コンテナを起動する時にそれらのファイルを自動で実行してくれるというPostgreSQLコンテナの性質を利用しています。

    ``` yaml
    version: '3'
    services:
      postgresql:
      image: postgres:13
      container_name: sample-db
      ports:
        - 65433:5432
      # この部分を追記
      volumes:
        - ./initdb.d:/docker-entrypoint-initdb.d
      environment:
        POSTGRES_USER: postgres
        POSTGRES_PASSWORD: passwd
        POSTGRES_DB: sample-db
    ```

4. コンテナの起動

    ここまで来れば、あとは意気揚々といつものコマンドを叩いて完了です。
    shが出てきたりなど若干複雑になってきましたが、ここまでで大体20秒くらいで実装できるかと思います。

    ``` bash
    docker compose up -d
    ```

    実際にデータが挿入されているか確認してみてください。

    ちなみに以下コマンドでコンテナを削除すると登録されているデータも全て削除されます。

    ``` bash
    docker compose down
    ```

## データの永続化

コンテナは揮発性という特性を持っており、基本的にコンテナへの変更などはコンテナが削除された際に消滅します。DBコンテナのデータも例外ではありません。
しかし開発環境用DBとしてDBコンテナを使う場合等、コンテナを削除してもデータを保持し続けて欲しい場合があります。

なので最後にデータの永続化の方法について紹介します。

1. ボリュームの設定

    今回も先程のdocker-composeに修正を加えていきます。
    ボリュームはコンテナ外にデータを保持し、コンテナを起動する際にそのボリュームをマウントするという処理を行います。

    ``` yaml
    version: '3'
    services:
      postgresql:
        image: postgres:13
        container_name: sample-db
        ports:
          - 65433:5432
        volumes:
          - ./initdb.d:/docker-entrypoint-initdb.d
        # この部分を追記
          - pgdata:/var/lib/postgresql/data
        environment:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: passwd
          POSTGRES_DB: sample-db
    # この部分を追記
    volumes:
    pgdata:
    ```

2. 永続化の確認

    データが永続化されていることを確認してみましょう。まずは慣れた手つきでコンテナを起動してください。

    ``` bash
    docker compose up -d
    ```

    次に、DBに何かしらの編集を行なった後、コンテナを削除します。

    ``` bash
    docker compose down
    ```

    もう一度、コンテナを起動します。

    ``` bash
    docker compose up -d
    ```

    この時、コンテナ削除前にDBに加えた編集内容が保持されているはずです。
    これでデータの永続化も完了です。歯を磨きながらでも10秒で実装できそうですね。

    ちなみにボリュームを削除した時は以下コマンドで削除可能です。

    ``` bash
    docker compose down -v
    ```

## まとめ

dockerは手軽に環境が作れる上に可搬性にも優れていて、環境構築のような煩雑な作業を軽減できるので個人的に結構好きな技術です。
個人的にはリポジトリをclone後にdocker compose up -dするだけで全ての開発環境が整うくらい整備されていると、とても嬉しい気持ちになります。
最近、個人開発で使用する機会があったり社内でDockerの勉強会に参加するなど、今更ながら触れる機会が多いのでまた何かDockerの別の内容の記事とかも書きたいな〜〜〜〜とは思っています。
（思っているだけです。）

ちなみに爆速と書いた手前、所要時間に短距離走の記録みたいな時間を記載していますが、絶対もっとかかる。

ここまで拙い長文にお付き合いいただきありがとうございます。
この記事が誰かの役に立つことを願っています。

おしまいです。
