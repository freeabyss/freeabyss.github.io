---
title: XML Schema 指示器 04
date: 2016-12-17 14:35:57
tags: [XML,Web,note]
categories: [XML]
---

## 指示器
通过指示器可以控制在文档中使用元素的方式。    
### Order 指示器
Order 用于定义元素的顺序
#### All
`<all>`指示器规定子元素可以按照任意顺序出现，且每个子元素必须只能出现一次。 
> 当使用 `<all>` 指示器时，你可以把 `<minOccurs>`设置为 0 或者 1，而只能把 `<maxOccurs>` 指示器设置为 1 
#### Choice
`<choice>`指示器规定可出现某个子元素或者可出现另外一个子元素（非此即彼）。 

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:choice>
      <xs:element name="employee" type="employee"/>
      <xs:element name="member" type="member"/>
    </xs:choice>
  </xs:complexType>
</xs:element>
```
> 如需设置子元素出现任意次数，可将 `<maxOccurs>`设置为 `unbounded`（无限次）。

#### Sequence
`<sequence>` 规定子元素必须按照特定的顺序出现。

### Occurrence 指示器
Occurrence 指示器用于定义某个元素出现的频率。    
> 对于所有的 "Order" 和 "Group" 指示器（any、all、choice、sequence、group name 以及 group reference），其中的 maxOccurs 以及 minOccurs 的默认值均为 1。

#### maxOccurs
`<maxOccurs>` 指示器可规定某个元素可出现的最大次数。如需使某个元素的出现次数不受限制，请使用`maxOccurs="unbounded"` 这个声明

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="full_name" type="xs:string"/>
      <xs:element name="child_name" type="xs:string" maxOccurs="10"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

#### minOccurs
`<minOccurs>` 指示器可规定某个元素能够出现的最小次数。

### Group指示器
Group 指示器用于定义相关的数批元素。       
您必须在 `group` 声明内部定义一个 `all`、`choice` 或者 `sequence` 元素。
#### 元素组
把 group 定义完毕以后，就可以在另一个定义中引用它了。

```xml
<xs:group name="persongroup">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
    <xs:element name="birthday" type="xs:date"/>
  </xs:sequence>
</xs:group>

<xs:element name="person" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:group ref="persongroup"/>
    <xs:element name="country" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

#### 属性组
已定义完毕属性组之后，就可以在另一个定义中引用它了。

```xml
<xs:attributeGroup name="personattrgroup">
  <xs:attribute name="firstname" type="xs:string"/>
  <xs:attribute name="lastname" type="xs:string"/>
  <xs:attribute name="birthday" type="xs:date"/>
</xs:attributeGroup>

<xs:element name="person">
  <xs:complexType>
    <xs:attributeGroup ref="personattrgroup"/>
  </xs:complexType>
</xs:element>
```