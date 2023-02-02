# Eddge Function

## function の作成とデプロイ

1. Supabase CLI のインストール

   ```bash
   brew install supabase/tap/supabase
   ```

2. Supabase にログイン

   ```bash
   supabase login
   ```

   アクセストークンが要求されるので以下を使用する。

   > sbp_4966be63c3026e0430712c4082838b95e84b9260

3. function の作成

   任意に移動しディレクトリで以下のコマンドを実行する。

   ```bash
   supabase functions new $FUNCTION_NAME
   ```

   ./supabase/functions/{FUNCTION_NAME}に index.ts が作成される。function の実装はこの index.ts 内に行う。

4. function のデプロイ

   ```bash
   supabase functions deploy $FUNCTION_NAME --project-ref $PROJECT_REFERENCE
   ```

   ESW プロジェクトのプロジェクトリファレンスは以下。

   > sdkknebpedyrhrazvyjz

5. function の削除

   ```bash
   supabase functions delete $FUNCTION_NAME
   ```
