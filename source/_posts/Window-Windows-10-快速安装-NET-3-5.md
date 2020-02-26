---
title: Window 10 快速安装.NET 3.5
date: 2017-01-16 11:49:25
tags: [Window,os,.net,tools]
categories: [Window]
---
1. 加载windows 10镜像文件到光驱
2. 按`Win`+`X`，选择'命令提示符(管理员)' 
3. 输入以下命令，其中`D:`代表光驱盘符 
```shell
dism.exe /online /enable-feature /featurename:netfx3 /Source:D:\sources\sxs
```
