---
title: javassist 版本兼容问题
date: 2017-08-15 10:08:15
tags: [Java, javassist,dubbo]
categories: [Java]
---
项目使用 dubbo 2.5.3 作为分布式框架。 今天运行项目时发现 javassist 抛出一以下异常：

`java.lang.RuntimeException: java.io.IOException: invalid constant type: 18`

回想起来周末的时候，顺手升级了 JDK，可能是因此造成的版本不兼容。根据网上回答，将 dubbo 引用的 javassist 版本升级到 3.18.0-GA 即可解决问题。

**注意** 不能升级到 3.20.0-GA ，我刚才开始也是直接升级到 3.20.0-GA，结果发现依然会抛出这个异常，直到降到 3.18.0-GA 才可以。



##### 升级到 3.18.0-GA 的办法 

dubbo 2.5.3 版本引用的 javassist 的版本是 3.15.0-GA ,在maven下升级到 3.18.0-GA 的方法就是排除 dubbo 的 javassist 依赖，重新引入 3.18.0-GA 版本的 javassist。

```xml
  <dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>dubbo</artifactId>
    <version>2.5.3</version>
    <exclusions>
      <exclusion>
        <groupId>org.javassist</groupId>
        <artifactId>javassist</artifactId>
      </exclusion>
    </exclusions>
</dependency>
<dependency>
  <groupId>org.javassist</groupId>
  <artifactId>javassist</artifactId>
  <version>3.18.0-GA</version>
</dependency>
```



另外贴一下，自己 JDK  的版本信息

```shell
java version "1.8.0_121"
Java(TM) SE Runtime Environment (build 1.8.0_121-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```



