# P(rocess) M(anager) 2

[[Github](https://github.com/Unitech/pm2)]
[[Outsider's Dev Story](https://blog.outsider.ne.kr/1197)]
[[Official Document CheatSheet](http://pm2.keymetrics.io/docs/usage/quick-start/#cheatsheet)]

## Install PM2

``` sh
$ sudo npm install pm2 -g
```

## Start an process

``` sh
# basic usage
$ pm2 start app.js --name "process-name"

# npm script run
$ pm2 start npm --name "process-name" -- run "script-name"
```

## Delete an process

``` sh
# delete process by name
$ pm2 delete [process-name|process-id]
```

## List / Show

``` sh
# list running process list
$ pm2 list

# show process information
$ pm2 show [process-name|process-id]
```