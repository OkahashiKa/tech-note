# TypeScript で変数の型を宣言する

## P1 概要

- var let const 違い ***
  - var: 再定義可, 再代入可
  - let: 再定義不可, 再代入可
  - const: 再定義不可, 再代入不可(嘘)
  - カーリーブラケット内でブロックスコープ定義できる（let, const）
  - ブロックスコープ内で巻き上げを行う
- let と const どちらが良い？ ***

## P2 TypeScript での型の概要

- リテラル型? ***

## P3 TypeScriptのプリミティブ

- テンプレート文字列 ***
  - ES2015で追加された

## P4 演習 列挙型

- Enumは未定義のkey（数値）からも値が取得できる（undrfined）ため型安全性に欠ける

## P5 TypeScript の any 型と unknown 型

- anyは任意の値を入れられると聞くと便利そうだが、何が問題なのか？ ***
  - any 型は型チェックから除外され、これらの値のプロパティの呼び出し、構築、アクセスを行う前にチェックを行う必要はありません。
- ここの型アサーションを消すとどうなるか

    ``` ts
    if (typeof randomValue === "string") {
        console.log((randomValue as string).toUpperCase());    //* Returns MATEO to the console.
    }
    ```

- 型ガードを消すとどうなるか。

## P6 TypeScript での共用体型と交差型

- 共用体型の別名は？
  - constでユニオン型は定義できるか
- オプションを使用すると number | undefined が定義される
- リテラル型を簡単に生成する方法？ ***

## P7 TypeScript のコレクション型

- タプルの中でもユニオン型が使える
- タプルを使わずに複数の型を配列に入れるには？
  - 型安全では無いので非推奨

## P8 TypeScript で型を使用する

### 1

1. 型をつける
2. constにする
3. テンプレート使う

### 2

- アロー構文でもかけますね