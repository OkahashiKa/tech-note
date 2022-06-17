# nodebrew

## Npm install by nodebrew

1. install nodebrew.

    ``` bash
    brew install nodebrew 
    ```

2. show version.

    ``` bash
    nodebrew -v
    ```

3. show node.js version.

    ``` bash
    nodebrew ls-remote 
    ```

4. install latest node.js.

    ``` bash
    nodebrew install-binary latest 
    ```

5. show version.

    ``` bash
    nodebrew list
    ```

6. set current version.

    ``` bash
    nodebrew use v16.3.0
    ```

7. show current version.

    ``` bash
    nodebrew list
    ```

8. add path.

    ``` bash
    export PATH=$PATH:/Users/kazuki.okahashi/.nodebrew/current/bin
    ```

9. show node version.

    ``` bash
    node -v
    ```

10. show npm version.

    ``` bash
    npm -v
    ```

## tops

``` bash
$ nodebrew install-binary latest
Fetching: https://nodejs.org/dist/v13.9.0/node-v13.9.0-darwin-x64.tar.gz
Warning: Failed to create the file
Warning: /Users/hiro/.nodebrew/src/v13.9.0/node-v13.9.0-darwin-x64.tar.gz: No 
Warning: such file or directory

curl: (23) Failed writing body (0 != 1020)
download failed: https://nodejs.org/dist/v13.9.0/node-v13.9.0-darwin-x64.tar.gz
```

1. mkdir

``` bash
mkdir -p ~/.nodebrew/src
```

## reference

- [](https://hirooooo-lab.com/development/install-node/)
