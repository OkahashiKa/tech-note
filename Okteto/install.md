# install Okteto CLI for mac

``` bash
brew install okteto
```

## oktetoへのログイン

``` bash
okteto ligin
# https://cloud.okteto.com (Okteto Cloud)を選択する。
```

## kubectlでOktetoの操作をできるようにする

``` bash
okteto context update-kubeconfig
```
