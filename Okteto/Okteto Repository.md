# Okteto Repository

基本的に公式のリファレンス通りに進めればいける。

- [Okteto Registry](https://okteto.com/docs/cloud/registry/)

## イメージのPush

1. Oktetoにログインする

    ``` bash
    okteto login
    # https://cloud.okteto.com (Okteto Cloud) を選択する
    ```

2. イメージビルド

    ``` bash
    docker build -t registry.cloud.okteto.net/$OKTETO_NAME_SPACE/$IMAGE_NAME:$TAG .
    ```

3. イメージのPush

    ``` bash
    docker push registry.cloud.okteto.net/$OKTETO_NAME_SPACE/$IMAGE_NAME:$TAG
    ```
