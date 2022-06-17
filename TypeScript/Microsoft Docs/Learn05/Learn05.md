# Learn05 TypeScript でジェネリックを定義する

## P2 ジェネリックの概要

- \<T>でジェネリックを定義するとパラメータによって型を定義するが、以下のような場合はどうなるか？

  ```ts
  function getArray<T>(items: T[]): T[] {
    return new Array<T>().concat(items);
  }

  const hoge = [1, "2", 3, true];
  console.log(getArray(hoge));
  ```

- 関数のパラメータを型推論させたいときに使う。

## P3 ジェネリック型のメソッドとプロパティを使用する

- ジェネリック制約

  ```ts
  type ValidTypes = string | number;

  function identity<T extends ValidTypes, U>(value: T, message: U): T {
    let result: T = value + value; // Error
    console.log(message);
    return result;
  }
  ```

- これエラーなくすには？

  ```ts
  function getPets<T, K extends keyof T>(pet: T, key: K) {
    return pet[key];
  }

  let pets1 = { cats: 4, dogs: 3, parrots: 1, fish: 6 };
  let pets2 = { 1: "cats", 2: "dogs", 3: "parrots", 4: "fish" };

  console.log(getPets(pets1, "fish")); // Returns 6
  console.log(getPets(pets2, "3")); // Error
  ```

## P4 演習 - インターフェイスとクラスでジェネリックを実装する

- インターフェースにもジェネリックは使用できる・

  ```ts
  interface Identity<T, U> {
    value: T;
    message: U;
  }
  ```

- 関数型にもジェネリックは使用できる。

  ```ts
  interface ProcessIdentity<T, U> {
    (value: T, message: U): T;
  }
  ```

## P6 ラボ - ジェネリックを使用してクラスを宣言する

- 以下のジェネリックを用いいたクラス内の AddOrUpdate に number と string を渡すには？

```ts
class DataStore<T> {
  private _data: Array<T> = new Array(10);

  AddOrUpdate(index: number, item: T) {
    if (index >= 0 && index < 10) {
      this._data[index] = item;
    }
  }

  GetData(index: number): T | null {
    console.log(typeof this._data[0]);
    console.log(typeof this._data[1]);
    if (index >= 0 && index < 10) {
      return this._data[index];
    }
    return null;
  }
}

let empIDs = new DataStore();
empIDs.AddOrUpdate(0, 50);
empIDs.AddOrUpdate(1, 65);
empIDs.AddOrUpdate(2, 89);
console.log(empIDs.GetData(0));
```
