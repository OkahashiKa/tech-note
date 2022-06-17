# Postgres standard command

## create user

``` bash
createuser -P [user-name]
```

## create database

``` bash
createdb [db-name] -O [owner-name]
```

## connent database

``` bash
psql -U [user-name] [db-name]
```

## create dump file

``` bash
pg_dump -h [host_name] -p [port] [database_name] > [backup_file_name]

# schema only
pg_dump -h [host_name] -p [port] --schema-only [database_name] > [backup_file_name]

# deta only
pg_dump -h [host_name] -p [port] --data-only [database_name] > [backup_file_name]
```
