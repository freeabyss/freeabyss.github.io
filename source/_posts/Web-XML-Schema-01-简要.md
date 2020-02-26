---
title: XML Schema 简要 01
date: 2016-12-16 22:41:28
tags: [XML,Web,note]
categories: [XML]
---
## 前言
XML Schema 语言即XML Schema Definition(XSD)，是基于XML格式，用于描述XML结构的文档，也是DTD的替代者。    

## XML Schema的作用
* 定义可出现在文档中的元素
* 定义可出现在文档中的属性
* 定义哪个元素是子元素 
* 定义子元素的次序
* 定义子元素的数目 
* 定义元素是否为空，或者是否可包含文本
* 定义元素和属性的数据类型
* 定义元素和属性的默认值以及固定值 

## XML Schema 引用
### schema 元素
`<schema>`元素是每一个XML Schema的根元素。    
```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="http://www.w3school.com.cn"
xmlns="http://www.w3school.com.cn"
elementFormDefault="qualified">
</xs:schema>
```
```xml
xmlns:xs="http://www.w3.org/2001/XMLSchema"
```
显示`schema`中用到的元素和 数据类型来自命名空间`http://www.w3.org/2001/XMLSchema`。同时它还规定了来自该命名空间的元素和数据类型应该使用前缀`xs`

```xml
targetNamespace="http://www.w3school.com.cn" 
```
显示被此`schema`定义的元素来自命名空间`http://www.w3school.com.cn`。    

```xml
xmlns="http://www.w3school.com.cn" 
```
指出默认的命名空间是`http://www.w3school.com.cn`

```xml
elementFormDefault="qualified" 
```
指出任何XML实例文档所使用的且在此schema中声明过的元素必须被命名空间限定。    

### 引用XSD 

```xml
<?xml version="1.0"?>
<note xmlns="http://www.w3school.com.cn"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.w3school.com.cn/note.xsd">

<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
```xml
xmlns="http://www.w3school.com.cn" 
```
规定了默认命名空间的声明。此声明会告知schema验证器，在此XML文档中使用的所有元素都被声明于`http://www.w3school.com.cn`这个命名空间。 一旦您拥有了可用的 XML Schema 实例命名空间： 
```xml
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
```
您就可以使用 schemaLocation 属性了。此属性有两个值。第一个值是需要使用的命名空间。第二个值是供命名空间使用的 XML schema 的位置：

