---
title: JavaScript编程风格
date: 2017-01-17 10:40:58
tags: [JavaScript,style guideline]
categories: [JavaScript]
---
## 编程风格
### 基本格式化
#### 缩进
使用4个空格进行缩进     
#### 语句结尾
不要省略分号     
#### 长度限制
每行的长度不要超过100字符  
#### 换行    
当需要换行时，最好在运算符后换行，下一行增加两个层级的缩进。

```javascript
callAFunction(document, element, window, "some string value", true, 123,
        navigator);
```
例外:当给变量赋值时，第二行的位置应当和赋值运算符的位置保持对齐，比如:      

```javascript
var result = something + anotherThing + yeAnotherTing + somethingElse + 
             anotherSomethingElse;
```
#### 空行
一般在以下场景中添加空行:      
* 方法之间
* 方法中的局部变量和第一条语句之间
* 在多行或单行注释之前
* 在方法内的逻辑片段之间插入空行，提高可读性

#### 命名
* 遵照小驼峰式大小写命名法，即由小写字母开始，后续每个单词首字母都大写   
* 变量尽量以名词作为前缀，函数以动词作为前缀  
* 尽量在变量名中体现出值的数据类型，例如`count`、`length`和`size`表明数据类型是数字，`name`、`title`和`message`表明数据类型是字符串
* 单个字符命名的变量，例如`i`、`j`和`k`通常在循环中使用   
##### 动词常见的约定
|动词| 含义|
|:--|:---|
|can| 函数返回一个布尔值|
|has| 函数返回一个布尔值|
|is | 函数返回一个布尔值|
|get| 函数返回一个非布尔值|
|set| 函数用来保存一个值|

##### 常量
使用大写字母和下划线 
##### 构造函数
构造函数即前面冠以`new`运算符的函数，遵循大驼峰命名法，即以大写字母开始，后续每个单词首字母都大写。     

#### 直接量字符串使用双引号，主要是因为方便在`Java`和`JavaScript`之间来回切换。    
禁止使用多行字符串，使用字符串连接符将字符串分成多份。     

```javascript
// bad
var longString = "Here's the sotry, of a man \
named Brady";
// good
var longString = "Here's the sotry, of a man " +
                 "named Brady";
```


### 注释
#### 单行注释
* 独占一行的注释，用来解释下一行代码。这行注释之前总是有一个空行，且缩进层级和下一行代码保持一致
* 代码行尾部的注释。代码结束到注释之间至少有一个缩进。并且不应当超过单行最大字符数限制，如果超过了应该将注释放在代码行上方
* 单行注释不应该以连续多行注释的形式出现，除非你注释掉一大段代码

#### 多行注释
* 多行注释推荐使用`Java`的风格

```javascript
/*
 * 这是一段多行注释
 * 这段注释包含两行文本
 */
```
* 多行注释和代码之间没有空行，注释上方应当有一行空行，并且缩进层级和下放的代码保持一致

#### 使用注释
* 难于理解的代码通常都应当加注释
* 可能被误认为错误的代码，应当添加注释，防止被好心的开发者“修复”

## 语句和表达式
无论何种情况下，所有块语句都应当使用花括号，包括:
* if...else
* for
* while
* do...while
* try...catch...finally

### 花括号的对齐方式
```javascript
if (condition) {
    doSomething();
} else {
    doSomethingElse();
}
```
### switch语句
#### 缩进
* 每条`case`语句相对于`switch`关键字都缩进一个层级
* 从第二条`case`语句开始，每条`case`语句前后各有一个空行
* 连续的`case`语句之间省略空行
* `default`语句是必须的

```javascript
switch (condition) {
    case "first":
         // 代码
         break;

    case "second":
    case "third":
         // 代码
         break;
    default: 
}
```

## 变量、函数和运算符
### 变量声明
推荐将局部变量的定义作为函数内第一条语句。 并且推荐使用单`var`语句风格，每个变量的初始化独占一行，没有初始值的变量放在`var`语句的尾部。 例如:

```javascript
function doSomethingWithItems(items) {
    var value = 10,
        result = value + 10,
        i, len;

    for (i=0, len=items.length; i<len; i++) {
        doSomething(items[i]);
    }
}
```

### 函数声明
* 推荐先声明函数，再使用
* 对于函数内的局部函数，应该紧接着变量声明之后声明，之间用空行隔开
* 函数声明禁止出现在`if`、`while`、`for`、`try...catch`、`switch`的语句块内

### 立即调用的函数
为了让立即执行的函数能够被一眼看出来，将函数用一对圆括号包裹起来。比如:    

```javascript
var value = (function() {
    // 函数体
    
    return {
        message: "Hi"
    }
}());
```

### 严格模式
最好不要在全局作用域使用`"use strict"`。 如果你将多个文件连接合并成一个文件时，当期中一个文件在全局作用域中启用了严格模式，则所有的代码都将以严格模式解析，这会很可能造成其他以非严格模式写的代码报错。     

```javascript
// bad
"use strict";
function doSomething() {
    // code 
}

// good
function doSomething() {
    "use strict";
    // code
}
```
推荐所有函数中都加上`"use strict"`。 
### 相等
因为强制类型转换的缘故，推荐使用`===`和`!==`，而不要使用`==`和`!=`。

### eval()
* 尽量避免使用`eval()`，如果无它法，尽量在严格模式下使用`eval()`
* 严禁使用`Function` 
* 可以使用`setTimeout()`和`setInterval()`，但不要用字符串形式，要用函数

### 原始包装类型
禁止使用原始包装类型

