# OpenAPI Tips

## OpenAPI Generator Tips

- Swaggerから自動生成されるクライアントソースはStatusCodeを204に設定するとレスポンスBodyは必ずnullになる。
- Swaggerから自動生成されるクライアントソースはDELETEメソッドにはリクエストBodyは必ずnullとなる。
- Swaggerから自動生成されるモデルクラスの各項目はデフォルトでEmitDefaultValueの属性がfalseになっている。
  - EmitDefaultValueの属性がfalseの場合、値が初期値(int:0, boolean:false)の項目は削除される。
