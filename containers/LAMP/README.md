# Container: LAMP
網頁伺服器 + Database

## 執行
```
docker-compose up -d
```

>Web Server
* Image：<依照需要自行放置>
* Port：80

>MySQL
* Image：mysql/mysql-server:8.0
* 帳號密碼設定
```
.env
```
>phpMyAdmin
* Image：phpmyadmin