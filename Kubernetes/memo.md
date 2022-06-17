# Kubernetes

## AKS上のPodへのアクセス

``` bash
> az login
// サブスクリプションが複数紐づいている場合はサブスクリプションを指定する。
> az account set --subscription <サブスクリプションID>
> az aks get-credentials --resource-group <リソースグループ名> --name <AKS名>
> kubectl config set-cluster <クラスタ名>
> kubectl config set-context --current --namespace=<ネームスペース名>
> kubectl get pods
> kubectl port-forward <ポッドID> [localhost:port]:5432
```
