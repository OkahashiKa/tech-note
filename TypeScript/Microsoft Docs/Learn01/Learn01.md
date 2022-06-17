# TypeScript を使用して JavaScript アプリケーションをビルドする

## TypeScript の使用を開始する

### P2 TypeScriptの概要

- ECMAScriptとは？ ***
  - ブラウザ戦争時代や、会社、開発者の思悪で独自の進化を遂げJavaScriptたちの標準化仕様
  - 2015(ES6)に本格的に標準化がなされる！以降毎年出てます！
    - let, const, アロー構文, 変数のスコープ（カーリブラケットで定義）, 分割代入, テンプレート構文, スプレット構文,

    ``` ts
    // 使用済みメソッドのパラメータの場合はQuickFixすると型推論される
    // letでの変数宣言の場合はnumberやstringが推論される
    // constでの変数宣言の場合はリテラル型で推論される
    function addNumbers(x, y) {
    return x + y;
    }

    console.log(addNumbers(3, 6));
    ```

- コンパイラ = TSC
  - TypeScriptで書かれているものをJavaScriptに変換する。
- トランスパイラ = Babel
  - 新しい記法を古い記法に変換しくれる。

### P5 TypeScript ファイルをコンパイルする

- TypeScript内にデフォルトで含まれているTSC(TypeScript Compiler)でTSファイルをJSファイルにコンパイルできる。

- このディレクトリで以下のコマンドを実行する

    ``` bash
    tsc sample.ts
    ```

- このプロセスで、TypeScript 固有のコード (型の宣言やインターフェイスなど) が削除されます。 さらに、Web ページから実行できるクリーンな JavaScript ファイルが生成され、これはブラウザーと互換性があります。
  - では何故TypeScriptで実装するのか？ ***

### P6 TypeScript プロジェクトを設定する

tsconfig.jsonのstrctをオンにすると厳格モードがオンになる。

``` json
"strict": true, 
```

- [“use strict”（厳格モード）を使うべきか？](https://analogic.jp/use-strict/)

- module01.htmlを開いて管理者画面のコンソールからTS内で定義した関数を実行してみる。

    ``` js
    addNumbers(2, 3);
    // => 5

    addNumbers(2, "there");
    // => 2there JSなので
    ```

- html内で読み込むファイルをtsファイルに変更してみる。
  - 型定義のところで怒られる。
