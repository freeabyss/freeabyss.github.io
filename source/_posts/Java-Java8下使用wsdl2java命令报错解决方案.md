---
title: Java8下使用wsdl2java命令报错解决方案
date: 2016-12-13 20:23:40
tags: [Java, wsdl, cxf]
categories: [Java]
---
## 环境
JDK:1.8     
apache-cxf: 2.7.x
## 描述
使用`wsdl2java`命令生产代码时抛出如下异常：       
```shell
java.lang.AssertionError: org.xml.sax.SAXParseException; systemId: jar:file:/path/to/glassfish/modules/jaxb-osgi.jar!/com/sun/tools/xjc/reader/xmlschema/bindinfo/binding.xsd; lineNumber: 52; columnNumber: 88; schema_reference: Failed to read schema document 'xjc.xsd', because'file' access is not allowed due to restriction set by the accessExternalSchema property.
```

## 解决方案
将以下内容保存为`jaxp.properties`文件，然后放到`%JAVA_HOME%\jre\lib`目录下。 
```shell
javax.xml.accessExternalSchema = all
```
引用 [http://stackoverflow.com/questions/23011547/webservice-client-generation-error-with-jdk8](http://stackoverflow.com/questions/23011547/webservice-client-generation-error-with-jdk8)