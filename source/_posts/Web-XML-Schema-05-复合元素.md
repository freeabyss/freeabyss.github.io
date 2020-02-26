---
title: XML Schema 复合元素 05
date: 2016-12-17 14:33:09
tags: [XML,Web,note]
categories: [XML]
---
## 复合元素
复合元素包含其他元素及属性的XML元素。 复合元素包括：   
* 空元素
* 包含其他元素的元素
* 仅包含文本的元素
* 包含元素和文本的元素
* 上述所有元素均可包含属性

### 仅包含元素的复合元素
复合元素声明有两种方式，第二种方式可用于其他元素。    

```xml
<xs:element name="employee">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

```xml
<xs:element name="employee" type="personinfo"/>
<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```
还可以在已有复合元素的基础上，添加一些元素。    

```xml
<xs:element name="employee" type="fullpersoninfo"/>
<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
<xs:complexType name="fullpersoninfo">
  <xs:complexContent>
    <xs:extension base="personinfo">
      <xs:sequence>
        <xs:element name="address" type="xs:string"/>
        <xs:element name="city" type="xs:string"/>
        <xs:element name="country" type="xs:string"/>
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```
`<sequence>`是指示器，这意味着子元素必须按照声明的次序出现。   

### 仅包含属性的复合元素
空的复合元素只能包含属性不能包含其他内容。   
一个空的XML元素:   

```xml
<product prodid="1345" />
```
声明如下：    

```xml
<xs:element name="product">
  <xs:complexType>
    <xs:complexContent>
      <xs:restriction base="xs:integer">
        <xs:attribute name="prodid" type="xs:positiveInteger"/>
      </xs:restriction>
    </xs:complexContent>
  </xs:complexType>
</xs:element>
```
或者更紧凑的写法

```xml
<xs:element name="product">
  <xs:complexType>
    <xs:attribute name="prodid" type="xs:positiveInteger"/>
  </xs:complexType>
</xs:element>
```

### 包含文本和属性的复合元素
```xml
<shoesize country="france">35</shoesize>
```
```xml
<xs:element name="shoesize">
  <xs:complexType>
    <xs:simpleContent>
      <xs:extension base="xs:integer">
        <xs:attribute name="country" type="xs:string" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
</xs:element>
```
> 请使用`extension` 或 `restriction` 元素来扩展或限制元素的基本简易类型

### 包含文本和元素的复合元素
```xml
<letter>
Dear Mr.<name>John Smith</name>.
Your order <orderid>1032</orderid>
will be shipped on <shipdate>2001-07-13</shipdate>.
</letter>
```
```xml
<xs:element name="letter">
  <xs:complexType mixed="true">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
      <xs:element name="orderid" type="xs:positiveInteger"/>
      <xs:element name="shipdate" type="xs:date"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```
> 为了使字符数据可以出现在 "letter" 的子元素之间，mixed 属性必须被设置为 "true"。
