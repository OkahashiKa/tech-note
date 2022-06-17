# ACR

## install kubernetes cli

``` Bash
brew install kubernetes-cli
```

## show kubernetes version

``` Bash
kubectl version
```

## show aks version list

``` Bash
az aks get-versions --location japaneast --output table
```

## create aks

``` Bash
az aks create \
-n $AKS_CLUSTER_NAME \
-g mycocktails \
--node-count 1 \
--kubernetes-version 1.21.2 \
--node-vm-size Standard_B4ms \
--generate-ssh-keys \
--service-principal $APP_ID \
--client-secret $SP_PASSWORD
```

## get aks credentials

``` Bash
az aks get-credentials --admin -g $RES_GROUP -n $AKS_CLUSTER_NAME
```

## show node list

``` Bash
kubectl get node

# all info
kubectl get node -o=wide
```

## show node detailinfo

``` Bash
kubectl describe node $NODE_NAME
```

## Refarence

- [AKSインスタンス作成時に生成されるリソースグループ](https://logico-jp.io/2020/01/15/generated-resource-groups-when-creating-aks-instance/)
