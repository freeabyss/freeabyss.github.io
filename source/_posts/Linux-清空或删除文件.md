---
title: Linux 清空或删除文件
date: 2016-12-09 22:35:00
tags: [Linux, shell]
categories: [shell]
---
## 使用重定向的方式清空文件
```shell
> access.log # 在Mac下没有成功
: > access.log # 在Mac下成功
cat /dev/null > access.log # 使用cat 显示/dev/null中的内容，然后重定向access.log文件中
cp /dev/null access.log # 复制/dev/null 的内容到access.log文件，达到清空的目的。
echo " " > access.log #使用echo 将空白字符重定向access.log中
echo > access.log # 同上
echo -n > access.log
```

> 在Linux中，`null`设备基本上被用来丢弃某个进程不再需要的输出流，或者作为某个输入流的空白文件。

## 使用`truncate`
`truncate`可用来将一个文件缩小或者扩展到某个给定的大小。Mac中不存在该命令
```shell
truncate -s 0 access.log #使用-s 指定文件大小
```
