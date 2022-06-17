# cron

定期的にジョブを自動的に実行するようにスケジュールするlinuxの機能。(定期バッチの実行やログの取得など…)
cronの操作には「crontab」コマンドを使用する。

## crontab

``` bash
## edit cron
crontab -e

## show cron
crontab -l

## remove cron
crontab -r

## select cron setting file
crontab [setting file path]
```

## How to write a cron file

``` bash
## [Minutes] [Hour] [day] [month] [day of the week] [command or pullpath]
## Initially it runs every minute.
* * * * * [command]

## example: Run getLog.sh at 23:59 every day. 
59 23 * * * getLog.sh

## example: # 1m, 6m, 11m, ……, 56m
1-56/5 * * * * getLog.sh
```

## Reference

- [【入門】cron（クロン）設定・書き方の基本](https://www.kagoya.jp/howto/rentalserver/cron/)
- [crontabの書き方](https://www.server-memo.net/tips/crontab.html)
- [cronの設定方法](https://qiita.com/hikouki/items/e744b3a4d356d2af12cf)

## Interesting

- [cron 指定時刻にシャットダウンする](http://meyon.jugem.jp/?eid=1005117)
- [MACにオリジナルの通知アラートを設定！遊びながらcrontabの使い方を習得しよう](https://liginc.co.jp/295876)
