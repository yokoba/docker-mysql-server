# MySQLをDockerで起動する

## 起動したDockerのMySQLに接続する
- dockerで構築したMySQLのあるホストから接続する場合<br>以下のように指定しないとエラーが出て接続できない
```
$ mysql -u root -proot
mysql: [Warning] Using a password on the command line interface can be insecure.
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)
```

### -h localhostを利用する場合
```
$ mysql -u root -p -h localhost --protocol tcp
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 26
Server version: 5.7.32 MySQL Community Server (GPL)
Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>

```

### -h 127.0.0.1を利用する場合(推奨)
```
[root@localhost sqltest]# mysql -u root -p -h 127.0.0.1
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 28
Server version: 5.7.32 MySQL Community Server (GPL)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

### 他の所から接続する場合(これは通常)
```
$ mysql -u root -proot -H localhost
```


### -h localhostの場合--protocol tcpが必要な理由
- MySQLでlocalhostと127.0.0.1の違い<br>
https://qiita.com/TanukiTam/items/f6a08740d0fcda0db7be

- localhostを利用した場合ソケット接続が利用されるらしい
