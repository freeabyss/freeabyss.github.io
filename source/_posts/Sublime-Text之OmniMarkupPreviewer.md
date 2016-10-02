---
title: Sublime Text之OmniMarkupPreviewer
date: 2016-09-13 21:37:44
tags: [sublime, markdown]
categories: [sublime]
---

# OmniMarkupPreviewer
## 功能概述

* 实时预览，多设备同时刷新
* 扩展语法
* MathJax 公式
* 文档内标题导航
* 支持HTML、PDF格式导出

OmniMarkdownPreviewer采用python-markdown解析，相关的扩展配置，请参阅[python-markdown](https://pythonhosted.org/Markdown/extensions/index.html)

## 快捷键

|快捷键| 说明|
|:--|:-|
|`option`+`command`+O|打开浏览器进行预览|

## 配置

| 配置| 说明|
|:--|:--|
|server_host|开启预览服务的IP地址，建议为本机固定IP，这样可实现局域网内的设备均可访问，不需要的话默认即可|
|server_port|访问端口号，默认即可|
|refresh_on_modified| 是否开启实时刷新，默认即可|
|refresh_on_modified_delay|刷新延时，单位毫秒，默认即可|
|refresh_on_saved|保存时刷新预览，默认即可|
|browser_command|设置预览的浏览器|
|html_template_name|预览模版|
|ignored_renderers|忽略标记语言的渲染器|
|mathjax_enabled|开启LaTex|
|renderer_options-MarkdownRenderer|渲染扩展，扩展Markdown的语法|

### 渲染说明

* attr_list ：开启文档内跳转
* footnotes ：文档脚注  
* codehilite：代码语法高亮     
* toc ：在文章开头自动生成目录，并附带跳转链接  
* strikeout：删除线   ~~ 删除线 ~~
* superscript ：上标  H^2^
* subscript：下标   H~2~  