# Azure Command Line Interface

Azure CLI は、Azure リソースをコマンドベースで作成および管理するためのコマンドセットです。
Azure Cloud Shell から実行するのが一般的ですが、WindowsServerやLinuxにもインストールすることで使用可能。

[公式ドキュメント](https://docs.microsoft.com/ja-jp/cli/azure/?view=azure-cli-latest)

## LinuxVM にAzure CLIをインストール

環境: Linux VM (Ubuntu18.04)

### オールインワンスクリプトでのインストール(推奨)

``` bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

### 手動インストール(上記方法が使えない場合)

1. 前提パッケージの取得

    ``` bash
    sudo apt-get upd
    sudo apt-get install ca-certificates curl apt-transport-https lsb-release gnupg
    ```

2. Microsoft の署名キーのインストール

    ``` bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null
    ```

3. Azure CLI リポジトリを追加

    ``` bash
    AZ_REPO=$(lsb_release -cs) echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" |
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

4. azure cli のインストール

    ``` bash
    sudo apt-get update
    sudo apt-get install azure-cli
    ```

## install azure cli for mac

``` bash
brew update && brew install azure-cli
```

## login

``` bash
az login
```

## install kubernetes cli

``` bash
sudo az aks install-cli
```

## show subscripsion list

``` bash
az account list
```

- [az account](https://docs.microsoft.com/ja-jp/cli/azure/account?view=azure-cli-latest)

## show resourse group list

``` bash
az group list
```

- [az group](https://docs.microsoft.com/ja-jp/cli/azure/group?view=azure-cli-latest)
