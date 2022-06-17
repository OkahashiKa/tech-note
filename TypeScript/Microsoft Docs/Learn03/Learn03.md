# TypeScript を使用して型指定された関数を開発する

## P4 パラメーターを使用する

- レスト構文
  - 同じ...を使う構文にスプレット構文というものがありますね。
    - 配列等を「展開」して他の変数に代入する

- 分割オブジェクト
  - パラメータのプロパティを消すとどうなる？
    - interfaceのプロパティを省略可能にすることで可能。

## P5 演習 - パラメーターを使用する

- 省略可能パラメータは必須パラメータの後でないと定義できないが、Interfaceの省略可能プロパティはどの位置でも定義できる。

## P6 演習 - 関数型を定義する

- モードセレクトのような実装ができる

    ``` typescript
    type calculator = (x: number, y: number) => number;

    let addNumbers: calculator = (x: number, y: number): number => x + y;
    let subtractNumbers: calculator = (x: number, y: number): number => x - y;
    console.log(doCalculation('subtract')(1, 2))
    ```

- 関数型はインターフェースで定義すると拡張可能。
