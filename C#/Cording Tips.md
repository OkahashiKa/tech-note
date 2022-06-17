# Cording Tips

## 配列、リストの比較

```C#
List list1 = new List<int> {1, 2, 3};
List list2 = new List<int> {1, 2, 3};

list1.SequenceEqual(list2);
```

ただし、配列の順序が異なる場合は比較できない。

## 配列、リストのソート

```C#
// list
List list = new List<int> {3, 2, 1};
list.sort();

Console.WriteLine(list); // [1, 2, 3]

// Array
int[] array = [3, 2, 1];
Array.sort(array);

Console.WriteLine(array); // [1, 2, 3]
```

### ?について

- C#の??（ダブルクエスチョンマーク）は null 合体演算子

  - null 合体演算子は「??」の左辺が null でなければ左辺を返し、null であれば右辺を返します。

    ```c#

    ```
