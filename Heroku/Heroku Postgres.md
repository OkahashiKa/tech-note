# Heroku Postgres

## Backup & Restore

1. show heroku version

    ``` Bash
    heroku version
    ```

2. backup heroku db

    ``` Bash
    heroku pg:backups -a [APP_NAME]
    ```

3. ?

    ``` Bash
    heroku pg:backups capture --app [APP_NAME]
    ```

4. ?

    ``` Bash
    heroku pg:backups:download [BACKUP_ID] -a [APP_NAME] -o [OUTPUT_DIR]
    ```

5. restore db

    ``` Bash
    pg_restore --verbose --clean --no-acl --no-owner -h [DB_HOST] -d [DB_NAME] latest.dump
    ```

## 尚、上記の方法ではリレーションが正しくリストアされなかったためpg_dumpを用いた以下の方法を推奨

``` Bash
pg_dump -d データベース名 -h ec2-xxxxxx.amazonaws.com -U ユーザ名 --schema-only -W > database.dump
```

``` Bash
psql [DB_NAME] < [DUMP_FILE_NAME]
```
