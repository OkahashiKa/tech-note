# homebrew

## Install homebrew

以下のリンク内のコマンド実行でインストール。

- [homebrew](https://brew.sh/index_ja)

``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Add homebrew path

以下のコマンドでPATHが通せる。

``` bash
export PATH="$PATH:/opt/homebrew/bin" 
```

しかしターミナルを閉じると設定がPATHが消えるため、
ターミナルを開くたびに再設定が必要。

### 解決策

1. open .zshrc file.

    ``` bash
    vi ~/.zshrc 
    ```

2. add path code.

    ``` bash
    export PATH=/opt/homebrew/bin:$PATH
    ```

3. reset.

    ``` bash
    source ~/.zshrc
    ```

4. show version.

    ``` bash
    brew -v
    ```

## reference

- [](https://chicog.me/articles/1/)
