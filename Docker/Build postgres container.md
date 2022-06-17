# Build postgres container

## simple build postgres container

1. run postgres container.

    ``` Bash
    docker run -d --name sample-db -p 5432:5432 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=passwd -e POSTGRES_DB=sample-db postgres:13
    ```

2. connection check.

    ``` Bash
    psql -h localhost -p 5432 -U postgres
    ```

## build postgres container with docker-compose

1. implement docker file.

    ``` Dockerfile
    # postgres:13.1を使用
    FROM postgres:13

    # ロケール設定
    RUN localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
    ENV LANG ja_JP.utf8
    ```

2. implement docker-compose file.

    ``` yaml
    version: '3'
    services:
    mycocktails-db:
        container_name: cocktails-db-container
        build: .
        ports:
        - 65432:5432
        environment:
        POSTGRES_USER: postgres
        POSTGRES_PASSWORD: passwd
    ```

3. up docker-docker-compose.

    ``` Bash
    docker-compose up -d
    ```

4. connection check.

    ``` Bash
    psql -h localhost -p 65432 -U postgres
    ```

## Build postgres container and set initial value

1. implement docker file.

    ``` Dockerfile
    # postgres:13.1を使用
    FROM postgres:13

    # ロケール設定
    RUN localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
    ENV LANG ja_JP.utf8
    ```

2. implement docker-compose file with volumes.

    ``` yaml
    version: '3'
    services:
    mycocktails-db:
        container_name: cocktails-db-container
        build: .
        ports:
           - 65432:5432
        environment:
            POSTGRES_USER: postgres
            POSTGRES_PASSWORD: passwd
        volumes:
            - ./docker-entrypoint-initdb.d:/docker-entrypoint-initdb.d
    ```

3. implement init.sh

    ``` Bash
    
    ```
