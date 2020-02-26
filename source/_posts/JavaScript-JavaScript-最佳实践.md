---
title: JavaScript 最佳实践
date: 2017-01-17 14:25:53
tags: [JavaScript, effective]
categories: [JavaScript]
---
## UI 松耦合
### 将JavaScript从CSS中抽离
IE8及更早版本的IE有一个特性，允许将JavaScript直接插入CSS中。虽然IE9已经不在支持这种特性，但应当注意不要在CSS中嵌入JavaScript代码

### 将CSS从JavaScript中抽离
所有的样式信息都应当保持在CSS中，当需要通过JavaScript来修改元素样式的时候，最佳方法是操作CSS的`className`。     
有一种情形可以例外:当需要给页面中的元素作定位，使其相对于另外一个元素或整个页面重新定位。这种计算是无法在CSS中完成的。    

### 将JavaScript从HTML中抽离
* 最好将所有的JavaScript代码都放入外置文件中，并在页面中通过`<script>`标签引用
* 在HTML页面中，禁止使用`on`属性挂载事件处理程序。应当使用方法来添加事件

### 将HTML从JavaScript中抽离
尽量避免将HTML嵌入JavaScript代码中。

## 避免使用全局变量
全局变量和全局函数带来很多问题，例如命名冲突、代码脆弱性、难以测试、意外的bug。    

### 零全局变量方式
如果你的代码运行时不需要于其他代码产生交互，可以使用零全局变量方式 

```javascript
(function(win) {
    "use strict";
    // body
}(window));
```
如果项目中使用jQuery框架的话，一般用`jQuery`代替`window`。 

## 事件处理
### 隔离应用逻辑
将应用逻辑从事件处理程序中抽离出来有两点好处:一是可重用，二是方便测试。  

```javascript 
// bad 
function handleClick(event) {
    var popup = document.getElementById("popup");
    popup.style.left = event.clientX + "px";
    popup.style.top = event.clientY + "px";
    popup.className = "reveal";
}
addListener(element, "click", handleClick);
// good
var MyApplication = {
    handleClick: function(event) {
        this.showPopup(event);
    },
    showPopup: function(event) {
        var popup = document.getElementById("popup");
        popup.style.left = event.clientX + "px";
        popup.style.top = event.clientY + "px";
        popup.className = "reveal";        
    }
}
addListener(element, "click", function(event){
    MyApplication.handleClick(event);
})
```
### 不要分发事件
上述实例代码还存在一个问题，即`event`被毫无节制地分发，应用逻辑不应当依赖于`event`对像，原因如下:      

* 方法接口没有表明那些数据是必要的。好的API应该明确清楚表明回调传值的用处以及需要传那些值 
* 最重要的一点是，如果想测试这个方法，必须重新创建一个`event`对象并将它作为参数传入。

最佳方法是让事件处理程序使用`event`对象来处理事件，然后拿到所有需要的数据传给应用逻辑。      
另外，如果需要对`event`执行任何必要的操作，包括阻止默认事件或阻止事件冒泡，都应该直接包含在事件处理程序中。  

```javascript
var MyApplication = {
    handleClick: function(event) {
        event.preventDefault();
        event.stopPropagation();

        this.showPopup(event.clientX, event.clientY);
    },
    showPopup: function(event) {
        var popup = document.getElementById("popup");
        popup.style.left = x + "px";
        popup.style.top = y +"px";
        popup.className = "reveal";
    }
}
```

## 避免“空比较”
### 检测原始值 
如果你希望一个值是字符串、数字、布尔值或`undefined`，最佳选择是使用`typeof`运算符。`typeof`的独特之处在于，将其用于一个未声明的变量也不会报错。      
`null`一般不应用于检测语句，简单的和`null`比较通常不会包含足够的信息以判断值的类型是否合法。 但是如果所期望的值真的是`null`，则可以直接和`null`比较。这时应当使用`===`或`!==` 。

```javascript
if (typeof name === "string") {
    anotherName = name.substirng(3);
}
if (typeof count === "number") {
    updateCount(count);
}
if (typeof found === "boolean" && found) {
    message("Found!");
}
if (typeof MyApp === "undefined") {
    MyApp = {};
}
// null
var element = document.getElementById("my-div");
if (element !== null) {
    element.className = "found";
}
```

### 检测引用值
* 杜绝使用`typeof`检测`null`的类型，因为`typeof null`会返回`object`
* 检测自定义类型或者内置类型可以使用`value instanceof Object`来判断，不过因为`instanceof`不仅检测对象的构造器，还检测原型链，因此使用时需注意 

### 检测函数
检测函数最好的方法是使用`typeof`。  

```javascript
function myFunc() {}
console.log(typeof myFunc === "function"); // true
```

### 检测数组
检测数组最优雅的解决方案是:   

```javascript
function isArray(value) {
    return Object.prototype.toString.call(value) === "[object Array]";
}
```
这种方式在识别内置对象时往往十分有用。    
ECMAScript5 已经将`Array.isArray`正式引入JavaScript。

### 检测属性
* 判断属性是否存在的最好办法是使用`in`运算符。`in`运算符仅仅简单的判断属性是否存在，而不会读取属性的值 
* `in`运算符同时会检测对象的原型，如果只想检测实例对象的某个属性是否存在，则使用`hasOwnProperty()`方法

## 将配置数据从代码中分离出来
配置数据示例:     

* URL
* 需要展现给用户的字符串
* 重复的值
* 设置(比如每页的配置项)
* 任何可能发生变更的值

最好将配置数据抽离出来，可以放在文件最前面，或者单独一个文件。好处是不用修改JavaScript源码已、方便修改和防止漏改。   

## 抛出自定义错误
### 抛出错误的方式
抛出错误时，最好抛出`Error`类型对象

```javascript
throw new Error('Something bad happened');
```

### 抛出错误的好处
抛出错误有助于调试，例如:

```javascript
function getDivs(element) {
    if (element && element.getElementsByTagName) {
        return element.getElementsByTagName("div");
    }else {
        throw new Error("getDivs() : Argument must be a DOM element.");
    }
}
```

### 何时检查错误
* 如果一个函数被已知的实体调用，错误检查很可能没有必要，一般情况下该函数为私有函数
* 如果不能确定函数被调用的所有地方，则需要进行一些错误检查
* 抛出错误最佳的地方是在工具函数中  
* 一旦修复了一个很难调试的错误，尝试增加一两个自定义错误，当再次发生错误时，这将有助于更容易的解决问题
* 如果正在编写代码，思考一下: “我希望[某些事情]不会发生，如果发生，我的代码会一团糟糕”。这时，如果“某些事情”发生，就抛出一个错误
* 如果正在编写的代码别人也会使用，思考一下他们使用的方式在特定的情况下抛出错误
* 抛出错误的目的不是防止错误，而是在错误发生时能更加容易地调试

### 错误类型
* 可以用`instanceof`判断错误类型，从而处理特定的错误
* 自定义错误类型可以区别于浏览器抛出的错误
* 不要将`try-catch`中的`catch`块留空



## 直接量
### 数字
禁止八进制直接量
### null
以下场景应当使用`null`
* 用来初始化一个变量
* 用来和一个已初始化的变量比较
* 当函数的入参和返回值

以下场景不应当使用`null`   
* 不要使用`null`来检测是否传入了某个参数 
* 不要用`null`来检测一个未初始化的变量  
理解`null`最好的方式是将它当作对象的占位符。    
### undefined
避免在代码中使用`undefined`。  尤其不要将一个变量赋值为`undefined`。

### 对象直接量
推荐使用对象直接量的方式创建一个对象。    

### 数组直接量
推荐使用数组直接量的方式创建数组

## 语句
### switch
任何情况下，都不应该省略`default`语句。    
