# psql cheat sheet

## show postgres version

``` psql
select version();
```

## around connect

### reconnect another database

``` psql
\c [db_name]
```

### disconnect postgres server

``` psql
\q
```

## around database

### show database list

``` psql
\l
```

### create database

``` psql
CREATE DATABASE [db_name];
```

### delete database

``` psql
DROP DATABASE [db_name]];
```

## around user

### show user list

``` psql
\du
```

## create user

``` bash
createuser -P [user-name]
```

### grant all privileges

``` psql
GRANT ALL PRIVILEGES ON DATABASE [db_name] TO [user_name];
```

## around table

### show table list

``` psql
\dt
```

At this time, the database must be selected.

## Tips

- データ型にSERIALが設定されているカラムを含むデータをinsertする際は、自動採番されるため対象カラムは値を指定しなくても良いが、カラム名を指定して挿入する構文を用いる必要がある。

pass + username + pepper(mycocktails)
