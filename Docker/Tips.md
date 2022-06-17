# Docker Tips

## docker-composeのvolumeで初期shが動かない

- 改行コードがCRLFになっていることを疑う。
  - 実際に遭遇した際に表示されたエラーは以下の通り。

    ``` bash
    /bin/bash^M: bad interpreter:
    ```

## standard_init_linux.go:228: exec user process caused: exec format error

- このエラーは、dockerイメージをビルドした M1 mac とコンテナを実行するマシンのCPUアーキテクチャが異なるために発生する。
  - amd64のCPUで実行できるようにdocker buildにオプションを指定する。

    ``` bash
    docker build --platform amd64 -t NAME(ここには好きな名前をつける) .
    ```

  - [M1 mac docker error: exec user process caused "exec format error"](https://qiita.com/keita_ogawa/items/e115c46f1c8caf6fd34d)]
