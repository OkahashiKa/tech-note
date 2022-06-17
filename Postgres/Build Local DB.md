# build local DB

## build local DB for mac

1. search postgres vrtsion

    ``` bash
    brew search postgresql
    ```

2. install postgres

    ``` bash
    brew install postgresql
    # バージョンを指定する場合は、postgresql@12のように記載する。
    ```

3. check postgres installed.

    ``` bash
    postgres --version
    ```

4. run local postgres.

    ```bash
    postgres -D /usr/local/var/postgres
    # バージョンを指定した場合はディレクトリ名が異なる場合がある。
    ```

5. check local postgres databases list.

    ```bash
    psql -l
    ```

## create postgres user

``` bash
createuser -P [user_name]
```

## create db

```bash
createdb [db_name] -O [user_name]
# パスワードを設定する場合は-Pオプションを使用する。
```

## delete db

### user dropdb command

1. show db list.

    ``` bash
    psql -l
    ```

2. delete db.

    ``` bash
    dropdb -h localhost -p 5432 -U postgres [db_name]
    ```

### use sql

1. connect target postgre server.

    ``` bash
    psql -h localhost -p 5432 -U postgres
    ```

2. show db list.

    ``` SQL
    psql=> \l
    ```

3. delete db.

    ``` SQL
    DROP DATABASE [db_name];
    ```
