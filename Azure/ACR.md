# Azure Containor Resistry

## ACRとは

Azure上に設置されるプライベートなコンテナレジストリ。
DockerHubのようにDockerイメージをpull,push出来き、認証にはAD認証を要するため機密性が高い。

## create acr

1. check acr name

    ``` bash
    az acr check-name -n $ACR_NAME
    ```

2. create acr

    ``` bash
    az acr create -g $GROUP_NAME -n $ACR_NAME --sku standard -l japaneast
    ```

3. show acr info

    ``` bash
    az acr show -n $ACR_NAME
    ```

## delete acr

``` bash
az acr delete --resource-group [resource group name] --name [acr name]
```

## get acr id in $ACR_ID

``` bash
ACR_ID=$(az acr show -n $ACR_NAME --query id --output tsv)
```

## create service principal

1. create service principal

    ``` bash
    # create service principal and setting role
    az ad sp create-for-rbac -n $SP_NAME --role Reader

    # create service principal and in $SP_PASSWORD
    SP_PASSWORD=$(az ad sp create-for-rbac -n $SP_NAME --role Reader --scopes $ACR_ID --query password --output tsv)
    ```

2. show list service principal

    ``` bash
    az ad sp list --display-name $SP_NAME
    ```

3. get service principal app id and in $APP_ID by $OBJECT_ID

    ``` bash
    APP_ID=$(az ad sp show --id $OBJECT_ID --query appId --output tsv)
    ```

## push docker image

1. login azure

    ``` bash
    az login
    ```

2. login acr

    ``` bash
    az acr login --name $ACR_NAME
    ```

3. show docker image

    ``` bash
    docker images
    ```

4. create tag

    ``` bash
    docker tag crmycocktails.azurecr.io/api/cocktails-api:latest crmycocktails.azurecr.io/mycocktails/api/cocktails-api:v1.0
    ```

5. push images

    ``` bash
    docker push crmycocktails.azurecr.io/api/cocktails-api:v1.0
    # pushするにはサーバー部分の設定をACRのサーバーに合わせる必要がある。
    #  -> エアリアスやタグ等を活用
    # latestでもpushできるが、バージョン管理したいためタグを切ってpushしたほうがよい。                             
    ```

## refarence

- [az acr](https://docs.microsoft.com/ja-jp/cli/azure/acr?view=azure-cli-latest)
- [JMESPath](https://docs.microsoft.com/ja-jp/cli/azure/query-azure-cli)
