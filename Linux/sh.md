# sh

## File descriptor

``` sh
# 1 = Standard output.
echo "ERROR" 1>> ${LOG_FILE}
```

- [シェルスクリプト ファイル記述子](https://qiita.com/blueskyarea/items/e8435bf6d101ccb1726c)
- [シェルスクリプトにおけるファイル記述子](https://qiita.com/yamazon/items/c78bc27d871489be9386)

## exit-status

- Get exit-status

    ``` sh
    JobExitStatus=${?}
    ```

- [終了ステータスとは？](https://shellscript.sunone.me/exit_status.html)

## `command`

- \`command` can exit command.

``` sh
$local = `command`
```
