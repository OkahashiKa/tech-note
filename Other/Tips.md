# Tips

## Check if the target port is already in use for mac

``` bash
lsof -i:5432
```

- [AzureAD、サブスクリプション、リソースグループの位置関係。](https://cloud.nissho-ele.co.jp/vdiblog/azuread_subscription_resourcegroups/)
- Azure Database for MySQLは初期でACLになにも登録されておらずSSHのみ許可になっている。
- Newtonsoft.json: デファクトスタンダートとして使われてきたjsonシリアライズライブラリ。Microsoftの推奨ではなくなった。
- npm install --save の--seveはpakage.jsonにインストールしたライブラリの情報を追加するオプションだが、npm verion5.0以降は自動で記載されるため省略可。

## オレオレ証明書

- 正式には自己署名証明書と呼ばれています。
公開鍵に署名をする際に、その公開鍵に対応した秘密鍵で署名を行った公開鍵証明書のことです。
通常はサーバ証明書は「信頼できる認証機関」が署名を行うのですが、それを自分で署名を行っているため、オレオレ証明書と呼ばれています
