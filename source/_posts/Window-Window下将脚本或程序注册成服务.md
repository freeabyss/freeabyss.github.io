---
title: Window下将脚本注册成服务
date: 2017-02-26 15:08:52
tags: [Window,Service]
categories: [Window]
---
1. 下载微软系统小工具 instsrv.exe 和 srvany.exe 至 C:\Windows\System32。[下载地址](https://www.microsoft.com/en-us/download/details.aspx?id=17657)    
2. 运行 Dos 命令代码：instsrv ServiceName C:\Windows\System32\srvany.exe    
    (ServiceName 即你自己定义的服务名称，可以是要作为系统服务启动的应用程序的名称。) 
3. 打开注册表，定位到下面的路径。 
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceName      
    (同样的 ServiceName 是你刚才安装服务时自定义的服务名称。) 
    如果该服务名下没有 Parameters 项目，则对服务名称项目右击新建项，名称为 Parameters，然后定位到 Parameters 项，新建以下几个字符串值。    
    名称 Application 值为你要作为服务运行的 BAT 文件地址。    
    名称 AppDirectory 值为你要作为服务运行的 BAT 文件所在文件夹路径。    
    名称 AppParameters 值为你要作为服务运行的 BAT 文件启动所需要的参数。     

注：instsrv ServiceName remove 命令可删除服务。