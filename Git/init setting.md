# Git init setting

- Gitの改行コードの設定は以下のようにするのがベター。

    ``` bash
    git config --global core.autocrlf input
    ```

- If you get an authentication error with GitClone, try the following command.

  ``` bash
  git config --global http.sslVerify false
  ```

## Reference

- [気をつけて！Git for Windowsにおける改行コード](https://qiita.com/uggds/items/00a1974ec4f115616580)
