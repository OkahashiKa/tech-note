# nvm

## install nvm

1. install nvm.

    ``` bash
    brew install nvm
    ```

2. make nvm dirctry.

    ``` bash
    mkdir ~/.nvm
    ```

3. add path.

    ``` bash
    vi ~/.zshrc

    export NVM_DIR="$HOME/.nvm"
    [ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
    [ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && . "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
    ```

4. show nvm version

    ``` bash
    nvm --version
    ```

## install node

1. show node version list.

    ``` bash
    nvm ls-remote
    ```

2. install node.

    ``` bash
    nvm i v14.17.4
    ```

3. show node version.

    ``` bash
    node -v
    ```

4. show current node version.

    ``` bash
    nvm current
    ```

5. show npm version.

    ``` bash
    npm -v
    ```

## uninstall node

``` bash
nvm uninstall v14.17.4
```

## release active

``` bash
nvm deactivate
```
