# RESTful API

基本的にパスでリソースを特定し、HTTPメソッドで処理内容を表すAPI。
例）
- ユーザー取得API: [GET]/api/v1/user/{user_id}
- ユーザー登録API: [POST]/api/v1/user/

複数削除のAPIはDELETEメソッドに対象IDのリストをBodyを持たせての実装は非推奨。（OpenAPI Generatorでは一部ソースが自動生成されない。）
→ [POST]/api/v1/user/bulk_deleteのようなエンドポイントを作成するのがベストプラクティス？