---
title: XML Schema 简易元素及属性 03
date: 2016-12-17 14:31:52
tags: [XML,Web,note]
categories: [XML]
---

## 简易元素
简易元素是指只包含文本的元素，不包括其他元素或者属性。  
#### 简易元素的语法
```xml
<xs:element name="xxx" type="yyy"/>
```
`xxx`是指元素的名称，`yyy`是指元素数据类型
例如 ：      
```xml
<lastname>Smith</lastname>
<age>28</age>
<dateborn>1980-03-27</dateborn>
``
对应       
```xml
<xs:element name="lastname" type="xs:string"/>
<xs:element name="age" type="xs:integer"/>
<xs:element name="dateborn" type="xs:date"/> 
```
#### 常用的数据类型
* xs:string
* xs:decimal
* xs:integer
* xs:boolean
* xs:date
* xs:time

#### 固定值和默认值
固定值会自动分配给元素，并且您无法规定另外一个值  
```xml
<xs:element name="color" type="xs:string" default="red"/>
<xs:element name="color" type="xs:string" fixed="red"/>
```

## 属性
简易元素无法拥有属性，但是属性总是作为简易类型被声明。     
#### 声明属性
```xml
<xs:attribute name="xxx" type="yyy"/>
```
属性的数据类型参见简易元素的数据类型。    
属性同样可以拥有固定值和默认值
```xml
<xs:attribute name="lang" type="xs:string" default="EN"/>
<xs:attribute name="lang" type="xs:string" fixed="EN"/>
```
属性默认是可选的，如规定属性必选，请使用`use`属性：    
```xml
<xs:attribute name="lang" type="xs:string" use="required"/>
```
