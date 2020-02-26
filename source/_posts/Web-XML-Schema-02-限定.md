---
title: XML Schema 限定 02
date: 2016-12-17 14:34:55
tags: [XML,Web,note]
categories: [XML]
---
## 限定
限定用于限制元素和属性可接受的值，对元素的限定被称为facet。    
关于限定的详细列子，请参考该链接[XSD 限定 / Facets](http://www.w3school.com.cn/schema/schema_facets.asp)    

### 限定定义  
```xml
<xs:element name="age">
<xs:simpleType>
  <xs:restriction base="xs:integer">
    <xs:minInclusive value="0"/>
    <xs:maxInclusive value="120"/>
  </xs:restriction>
</xs:simpleType>
</xs:element>   
```
上面的列子定义了`age`元素的值，不能低于0或者高于120.下面的列子具有同样的效果，只是类型`ageType`可被其他元素使用。 

```xml
<xs:element name="age" type="ageType">
<xs:simpleType name="ageType">
  <xs:restriction base="xs:integer">
    <xs:minInclusive value="0"/>
    <xs:maxInclusive value="120"/>
  </xs:restriction>
</xs:simpleType>
```

### 枚举约束
将XML元素的内容限制为一组可接受的值。    

```xml
<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>
```
### 数据类型限定
|限定|描述|取值|
|:--|:--|:--|
|enumeration   | 定义可接受值的一个列表||
|fractionDigits  |定义所允许的最大的小数位数。必须大于等于 0。||
|length  |定义所允许的字符或者列表项目的精确数目。必须大于或等于 0。||
|maxExclusive   | 定义数值的上限。所允许的值必须小于此值。||
|maxInclusive  |  定义数值的上限。所允许的值必须小于或等于此值。||
|maxLength  | 定义所允许的字符或者列表项目的最大数目。必须大于或等于 0。||
|minExclusive  |  定义数值的下限。所允许的值必需大于此值。||
|minInclusive  |  定义数值的下限。所允许的值必需大于或等于此值。||
|minLength  | 定义所允许的字符或者列表项目的最小数目。必须大于或等于 0。||
|pattern |定义可接受的字符的精确序列。||
|totalDigits |定义所允许的阿拉伯数字的精确位数。必须大于 0。||
|whiteSpace | 定义空白字符（换行、回车、空格以及制表符）的处理方式。||

> whiteSpace的取值：  
> 
> * collapse:移除所有空白字符（换行、回车、空格以及制表符会被替换为空格，开头和结尾的空格会被移除，而多个连续的空格会被缩减为一个单一的空格)
> * replace:除所有空白字符（换行、回车、空格以及制表符)
> * preserve:不会移除任何空白字符
