
# ASP.NET core

## Scaffolding

### generate entity class library

1. クラスライブラリ(.NET core)の作成
   - entities に空のクラスライブラリを作成する。
   - 必要なパッケージを導入する。
     - Microsoft.EntityFrameworkCore
     - Microsoft.EntityFrameworkCore.Design
     - Microsoft.EntityFrameworkCore.Tools
     - Npgsql.EntityFrameworkCore.PostgreSQL

2. Scaffoldの実行
   - entities/garagarapon.library.entities で以下のコマンドを実行する。

      ``` bash
      dotnet ef dbcontext scaffold "$CONNECTION_STRING" Npgsql.EntityFrameworkCore.PostgreSQL --context-dir Models --output-dir Models --context $CONTEXT_NAME
      ```

3. 必要があれば適宜slnのバージョン情報を更新する。
4. packageの作成
   - プロジェクトファイルと同じディレクトリで以下のコマンドを実行

      ``` Bash
      dotnet pack
      ```

5. プロジェクトの.csprojと同じフォルダにnuget.configを作成し対象のAzure Artifactsの接続先情報を記載する。
6. packageのAzure DevOps Artifacts へのPush
   1. Azure DevOps Artifacts からCreate Feed を選択し参照スコープの設定を行う。
   2. Connect to Feed からDotnet を選択する。
   3. プロジェクトファイルと同ディレクトリで前項目のPublish packages欄に記載のコマンドを実行

      ``` Bash
      dotnet nuget push --interactive --source "$ARTIFACT_NAME" --api-key az bin/Debug/$PACKAGE_NAME
      ```

   4. Powershell 上に表示されるURLとコードをブラウザ上で入力しAD認証を行う。

## install nuget package

1. VisualStadioのNugetパッケージの管理からパッケージソースの追加を選択。
2. 右上のパッケージソースの設定からパッケージソースを追加し以下の情報を入力する。
   > 名前: 追加するパッケージ名
   > ソース: <https://pkgs.dev.azure.com/DevOpsDemo20201729/Garapon-Api-Test/_packaging/ppt-garapon-project/nuget/v3/index.json>
3. パッケージ管理画面から参照したいNugetPackageをインストールする。

## CORS

- [CORSエラーってなに？どうすれば解決するの？](https://qiita.com/hgaiji/items/fabe6a23d564b20ad558)
- [ASP.NET Core でクロスオリジン要求 (CORS) を有効にする](https://docs.microsoft.com/ja-jp/aspnet/core/security/cors?view=aspnetcore-5.0)
- [CORS Policy 違反と，Preflight request (OPTIONS) について](https://blog.foresta.me/posts/http_preflight_request/)
- [Example commit log](https://dev.azure.com/OkahashiKa/MyCocktails/_git/MyCocktails/commit/357e28deb42cac969fdc43ea504ecda73c94417b?refName=refs%2Fheads%2Ffeature%2Ftask80&path=%2F20.api%2F20.source%2F20.cocktail%2Fmycocktails.api.cocktailApi%2FStartup.cs&_a=compare)

