# Angular Tips

## Ngxs Tips

- ルートモジュールにStoreをimportする際はStoreで管理するStateを配列で渡す。

    ``` angular
    NgxsModule.forRoot([SampleState]),
    ```

## multiple subscribe

- [【Angular】複数の非同期処理完了後の処理はforkJoin()を使おう](https://qiita.com/evekaso/items/3448e5752ec83ce2efa6)

## use observable object in template

``` angular
$deta | async as deta
```

## show object value in template

``` angular
object | json
```
