---
title: XML简要
date: 2016-12-15 21:44:31
update: 2016-12-16 22:34:00
tags: [XML,Web,note]
categories: [XML]
---
## 前言
XML是可扩展标记语言，本文整理自[W3School](http://www.w3school.com.cn/xml/index.asp)。    
关于XML的简介、用途以及与HTML的区别，请参考以下链接，本文只列出XML的要点：    
[XML简介](http://www.w3school.com.cn/xml/xml_intro.asp)     
[XML用途](http://www.w3school.com.cn/xml/xml_usedfor.asp)

## 语法
* XML文档的第一行为XML声明，定义了XML的版本和使用的编码。
* 第二行为描述文档的根元素，XML文档必须包含根元素，该元素是所有其他元素的父元素。
* 所有元素均可拥有文本内容、属性(类似HTML)以及子元素
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<note>
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
* 所有元素必须有关闭标签
* XML对大小写敏感   
* XML必须正确的嵌套
* XML的属性值须加引号，单引号和双引号均可使用
* XML的注释为`<!--  -->`，同HTML一样
* XML中空格会保留，HTML会把多个连续的空格裁减为一个
* XML以`LF`存储换行。`CR`回车符，`LF`换行符

### XML命名规则及最佳实践
* 名称可以含字母、数字以及其他的字符 
* 名称不能以数字或标点符号开始
* 名称不能以字符`xml`、`XML`、`Xml`等开始
* 名称不能包含空格
* 避免使用`-`、`.`、`:`字符。最好使用字母、数字以及`_`下划线

### XML属性
* 尽量使用元素来描述数据，仅仅使用属性提供与数据无关的信息
* 元数据应当存储为属性，而数据本身应当存储为元素

### XML验证
* DTD文档用于定义XML文档的结构
* SchemaDTD的代替者
* 如果XML文档存在错误，那么程序不应该继续处理这个文档

### XML 样式
* XML可以引用CSS样式格式化XML，但不推荐使用该方法，W3C推荐使用XSLT
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<?xml-stylesheet type="text/css" href="cd_catalog.css"?>
<CATALOG>
  <CD>
    <TITLE>Empire Burlesque</TITLE>
    <ARTIST>Bob Dylan</ARTIST>
    <COUNTRY>USA</COUNTRY>
    <COMPANY>Columbia</COMPANY>
    <PRICE>10.90</PRICE>
    <YEAR>1985</YEAR>
  </CD>
  <CD>
    <TITLE>Hide your heart</TITLE>
    <ARTIST>Bonnie Tyler</ARTIST>
    <COUNTRY>UK</COUNTRY>
    <COMPANY>CBS Records</COMPANY>
    <PRICE>9.90</PRICE>
    <YEAR>1988</YEAR>
  </CD>
</CATALOG>
```
* XSLT是首选的XML样式表语言
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<?xml-stylesheet type="text/xsl" href="simple.xsl"?>
<breakfast_menu>
  <food>
    <name>Belgian Waffles</name>
    <price>$5.95</price>
    <description>
       two of our famous Belgian Waffles
    </description>
    <calories>650</calories>
  </food>
</breakfast_menu>
```
### XML 命名空间
当两个相同的XML文档被一起使用时，如果两个文档包含不同内容和定义的相同元素，就会发送命名冲突。 为了避免该问题，引入了命名空间的概念。    
#### 通过使用前缀来避免命名冲突 
```xml
<h:table xmlns:h="http://www.w3.org/TR/html4/">
   <h:tr>
   <h:td>Apples</h:td>
   <h:td>Bananas</h:td>
   </h:tr>
</h:table>

<f:table xmlns:f="http://www.w3school.com.cn/furniture">
   <f:name>African Coffee Table</f:name>
   <f:width>80</f:width>
   <f:length>120</f:length>
</f:table>
```
其中`xmlns`属性为前缀赋予了一个与某个命名空间相关联的限定名称。(可以不使用`xmlns`，仅仅使用前缀来避免命名冲突)

#### 命名空间属性
命名空间属性被放置于元素的开始标签中，并使用以下语法：   
```xml
xmlns:namespace-prefix="namespaceURI"
```
#### 默认的命名空间
为元素定义默认的命名空间可以让我们省去在所有的子元素中使用前缀的工作。
```xml
<table xmlns="http://www.w3.org/TR/html4/">
   <tr>
   <td>Apples</td>
   <td>Bananas</td>
   </tr>
</table>
<table xmlns="http://www.w3school.com.cn/furniture">
   <name>African Coffee Table</name>
   <width>80</width>
   <length>120</length>
</table>
```
### CDATA
CDATA部分的所有内容都会被解析器忽略。     
CDATA部分不能包含字符串`]]>`。也不允许嵌套的CDATA。      
标记CDATA部分结尾的`]]>`不能包含空格或折行。  
```xml
<script>
<![CDATA[
function matchwo(a,b)
{
if (a < b && a < 0) then
  {
  return 1;
  }
else
  {
  return 0;
  }
}
]]>
</script>
```



