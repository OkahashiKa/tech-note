# Azure VirrtualMachines

## Azure VM とは

説明しよう「VM」とは「VirtualMachines」の略なのである。

----

## 多重化構成のVMの構築

使用リソース

- VM(main)
- VM(sub)
- LoadBarancer(ApplicationGateWay)

### 留意点

- VMと負荷分散リソースのSKUは統一する必要がある。
- 複数のVMで負荷分散する場合は可用性セットを作成し、同じ可用性セットの中に配置する必要がある。
  - 可用性セットの中には更新ドメインと障害ドメインが存在する。
  - 可用性セットの設定はVM作成時にしかできないため注意が必要。

----

## Azure VM for Linux でDocker環境構築

環境: Linux(Ubuntu18.04)

- 前提パッケージの取得
  - apt-transport-https
  - ca-certificates
  - curl
  - gnupg-agent
  - software-properties-common

  ```command:title
  sudo apt-get update
  sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
  ```

- GPG公開鍵のインストール

    ``` bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

- 鍵のFingerPrintを確認

    ``` bash
    $ sudo apt-key fingerprint 0EBFCD88
    pub   rsa4096 2017-02-22 [SCEA]
            9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub   rsa4096 2017-02-22 [S]
    ```

- aptリポジトリの追加

    ``` bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

- Docker-Engineのインストール

    ``` bash
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```
