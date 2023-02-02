# xUnit

xUnit とは.NET 用の無料オープンソーステストツールです。

[https://learn.microsoft.com/ja-jp/dotnet/core/testing/unit-testing-with-dotnet-test]

## コードカバレッジ

コードカバレッジとは、単体テストで実行する、行、分岐、またはメソッドのいずれかのコード量の尺度です。 たとえば、条件分岐が (分岐 a と分岐 b の) 2 つしかない単純なアプリケーションのコードで、条件付き分岐 a を単体テストで検証する場合、分岐のコードカバレッジは 50% と報告されます。

### ReportGenerator を用いたカバレッジレポートの生成

1. テストの実行

   実行するテストプロジェクト配下で以下のコマンドを実行する。

   ```bash
   dotnet test --collect:"XPlat Code Coverage"
   ```

   `--collect:"XPlat Code Coverage"`のオプションを付与することでコードカバレッジが記載された XML が出力される。
   ただ、この XML 形式ではとても人間が読めるものではないので、人間が読める形に変換を行う。

2. ReportGenerator のインストール

   以下のコマンドで ReportGenerator のインストールを行う。既にインスール済の場合は不要。

   ```bash
   dotnet tool install -g dotnet-reportgenerator-globaltool
   ```

3. カバレッジレポートの出力

   以下のコマンドで 1 で生成した XML からカバレッジレポートを出力する。
   ファイル名には、TestResults 内に生成されたファイル名をコピーする。

   ```bash
   reportgenerator -reports:".\TestResults\{ファイル名}\coverage.cobertura.xml" -targetdir:"coveragereport" -reporttypes:Html
   ```

4. カバレッジレポートの確認

   テストプロジェクト配下に生成された coveragereport ファイルの index.html を開くことでコードカバレッジを確認することが可能。
