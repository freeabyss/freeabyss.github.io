---
title: The server time zone value 'CST' is unrecognized or represents more than one time zone.
date: 2017-02-26 17:03:15
tags: [MySQL,error]
categories: [MySQL]
---
## 错误代码
```shell
The server time zone value 'CST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
```

## 解决方案
连接时，指定时区    

```shell
jdbc:mysql://localhost:3306/blog?serverTimezone=UTC
```

## 环境 

* jdk.18
* mysql-connector-java 6.0.2
* jetty
* idea 15
* mysql 5.7.11
