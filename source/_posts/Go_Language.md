[TOC]

## Go 构建

环境变量 GOPATH 的值是一个目录的路径，也可以包含多个目录路径，每个目录都代表 Go 语言的一个工作区。这些工作区用于放置 Go 语言的源码文件、归档文件、可执行文件。



### Go 语言源码的组织方式

Go 语言的源码是以代码包为基本组织单位的。在文件系统中这些代码包其实是与目录一一对应的。 

每个代码包都有一个导入路径，导入路径是其他代码在使用该包中的程序实体时需要引入的路径。如下所示：

```go

import "github.com/labstack/echo"

```

在工作区一个代码包的导入路径实际上就是从`src`子目录，到该包的实际存储位置的相对路径。 

所以，Go 语言源码的组织方式就是以缓解变量 GOPATH、工作区、`src目录`和代码包为主线。 



### 源码安装后的结果

* 源码文件放在工作区的`src` 子目录下。

* 归档文件放在该工作区的`pkg`子目录下，某个代码包产生的源码文件与归档文件同名。 导入路径为`github.com/labstack/echo`代码包的归档文件路径为`pkg/linux_amd64/github.com/labstack/echo.a`

* 可执行文件放在该工作区的`bin`子目录下。



### 理解构建和安装的过程

#### go build

`go build`是构建命令，会执行编译、打包等操作，并且这些操作的结果会放在某个临时目录中。 

* 如果构建的是库源码文件，那么操作的结果文件只会存放于临时目录中，这里的构建的主要意义在于检查和验证。

* 如果构建的是命令源码文件，那么操作的结果会被搬运到那个源码文件所在的目录中。 

##### go build 常用选项

`go build` 默认不会编译目标代码包所依赖的哪些代码包。当然如果所依赖的代码包的归档文件不存在或者源码文件有了变化还是会被编译的。 

`-a` 强制编译所依赖的代码包，包括所依赖的标准库中的代码包。加入`-i`还可以安装他们的归档文件。 

`-x` 可以看到 `go build`命令具体都执行了哪些操作。 

`-n` 只查看执行了哪些操作，而不执行它们。

`-v` 可以看到`go build`命令编译的代码包的名称，可配合`-a`标记搭配使用。 



#### go install

`go install` 执行安装操作之前会先执行构建，然后还会进行连接操作，并且把结果文件搬运到指定目录。

* 如果安装的是库源码文件，那么结果文件会被搬运到它所在工作区的`pkg`目录下的某个子目录中。 

* 如果安装的是命令源码文件，那么结果文件会被搬运到它所在工作区的`bin`目录中，或者环境变量`GOBIN`执行的目录。

构建和安装操作不同之处在于结果文件被搬运的位置。 



#### go get

命令 `go get`会自动从一些主流公用代码仓库下载目标代码包，并把它们安装到`GOPATH`包含的第一工作区的相应目录中。

如果存在`GOBIN`，那么仅包含命令源码文件的代码包会被安装到`GOBIN`指向的目录。 

**常用标记**

* `-u` 强制下载安装代码包

* `-d` 只下载代码包，不安装

* `-fix` 下载代码包后，先运行一个根据当前 go 版本修正代码的工具，然后再安装代码包

* `-t` 同时下载测试所需的代码包

* `-insecure` 允许通过非安全的网络协议下载和安装代码包，例如 HTTP



####  自定义代码包导入路径

原本代码包的导入路径为：`github.com/golang/sync/semaphore`，如果在源码文件的包声明语句的右边加入导入注释

```go 

package semaphore // import "golang.org/x/sync/semaphore"

```

即可使用`golang.org/x/sync/semaphore`作为包的导入路径。 

```shell

go get golang.org/x/sync/semaphore

```

程序实体是变量、常量、函数、结构体和接口的统称。

### 如何把命令源码文件中的代码拆分到其他源码文件中

在命令源码文件同目录下新建源码文件，包名与命令源码文件保持一致。然后命令源码文件可直接调用新建源码文件中的函数（函数名小写）。 

* 同目录下的源码文件的代码包声明语句要一致。也就是说，他们属于同一个代码包。 

* 如何目录中有命令源码文件，那么其他种类的源码文件也应该声明属于 main 包。

* 源码文件声明的代码包名可以与其所在的目录的名称不同。 构建时生产的结果文件的主名称与其父目录的名称一致。但为了混乱一般代码包名和目录名保持一致。



### 怎么把命令源码文件中的代码拆分到其他代码包中

源码文件所在的目录相对于 src 目录的相对路径就是它的代码包导入路径，而实际使用其程序实体时给定的限定符要与它声明所属的代码包名称对应。

* 包名与源码文件所在的目录名保持一致。

* 将相对于 src 目录的相对路径作为导入路径

* 将需要对外使用的方法首字母大写。 



### import导入路径最后一级相同

* 如果声明的包名相同，则引发冲突，

* 如果包名不同则不会冲突

####  包名冲突的解决办法

* 设置别名，`import (b "fmt") ` 
* 导入点操作 , `import (. "fmt")` ，调用时不需要包名，可直接调用函数
* 只引入包而没有在代码中实际调用，`import (_ "fmt")`

### 命令源码文件

源码文件由命令源码文件、库源码文件、测试源码文件组成。 

命令源码文件可以通过构建或安装生成与其对应的可执行文件，后者一般会与该命令源码文件的直接父级目录同名。

例如源码文件属于`main`包，且包含一个无参数声明且无结果声明的`main`函数，那么就是命令源码文件。

对于一个独立的程序来说，命令源码文件有且只能有一个。 

#### 命令源码文件如何接受参数

Go 语言标准库中有一个代码包专门用于接收和解析命令参数，这个代码包叫做`flag`。

```go

import (
    "flag"
    "fmt"
)
var name string
func init() {
    flag.StringVar(&name, "name", "everyone", "The greeting object.")
}
func main() {
    flag.Parse()
    fmt.Printf("Hello , %s!\n", name)
}

```

可以使用`help`查看参数说明 。 `go run demo.go --help`。

`go build demo.go` 在当前目录下构建一个可执行文件。 

`go run demo.go` 也会先构建一个可执行文件放在临时目录，然后执行该文件。

### 自定义命令源码文件的参数说明

#### 使用 flag.Usage

```go

flag.Usage = func() {

    fmt.Fprintf(os.Stderr, "Usage of %s:\n", "question")

    flag.PrintDefaults()

}

```

该代码要放在`flag.Parse()`之前，当 运行`go run demo.go --help`时，`Fprintf`的内容将输出到终端上。 

#### flag.CommandLine

我们调用`flag`包的一些函数的时候，实际上是在调用`flag.CommandLine`变量的对应方法。对`flag.CommandLine`重新赋值可以更深层次的定制当前命令源码文件的参数说明。 在`init()`函数开始处添加以下代码：

```go

    flag.CommandLine = flag.NewFlagSet("", flag.ExitOnError)
    flag.CommandLine.Usage = func() {
        fmt.Fprintf(os.Stderr, "Usage of %s:\n", "question")
        flag.PrintDefaults()
    }

```



### 私有的命令参数容器

好处是保留了定制命令参数容器的灵活性，且不会影响全局变量`flag.CommandLine`

```go

package main
import (
    "flag"
    "fmt"
    "os"
)
var name string
var cmdLine = flag.NewFlagSet("question", flag.ExitOnError)
func init() {
    cmdLine.StringVar(&name, "name", "everyone", "The greeting object.")
}
func main() {
    cmdLine.Parse(os.Args[1:])
    fmt.Printf("Hello , %s!\n", name)
}
```



### Go 原理

Go 是按值调用的，调用函数接收到的是实参的一个副本，并不是实参的引用。

`golang.org/x/...`下的仓库都由 Go 团队负责设计和维护。这些包不属于标准库。

前缀`Must`开头的函数表示不应该接受的不正确的值，例如`template.Must`

Go 语言中封装的单元是包而不是类型。

要封装一个对象，必须使用结构体。

## 基本概念

* 每个 Go 程序都是由包构成，通过`import`导入包，按照约定包名与导入路径的最后一个元素一致，例如`import "fmt"`、`import "math/rand"`。
* 多个导入语句可以合并

```go

import (

    "fmt"

    "math"

)

```

* 导出的函数首字母必须大写，类似于 Java 的`public`方法。

* 函数声明

```go

func add (x int, y int) int {
    return x + y
}

```

* 多个连续相同类型的参数，类型名可以合并，例如`func add( x, y int) int ;`

* 返回值可以返回任意数量的返回值

```go

func swap ( x, y string) (string, string) {

    return y, x

}

func main() {

    a, b := swap("hello", "world!")

}

```

* Go 的返回值可被命名，会被视为定义在函数顶部的变量。 采用没有参数的`return`语句返回已命名的返回值。 

```go

func split(sum int) (x, y int) {

    x = sum * 4 / 9

    y = sum - x

    return

}

```

* `var` 用于声明变量，可声明变量列表，类型在最后。 可以出现在包或函数级别。

* 变量声明可以包含初始值，每个变量对应一个。初始化声明时可省略类型，从初始值中获得类型。

```go

var i, j int = 1, 2

var c, python, java = true, false, "no!"

```

* 短声明用于声明局部变量可在类型明确的地方代替`var`声明。 

```go

var i, j int =1, 2

k := 3

```

* 表达式 `new(T)` 创建一个未命名的 T类型变量，初始化为 T 类型的零值，并返回其地址，地址类型 `*T`，每次调用 new 都会返回不同的地址，但是两个变量的类型不携带任何信息且是零值，例如 `struct{}` `int[0]` ，在当前实现中有相同地址。

* 函数外的每个语句必须以关键字开始，例如`var`、`func`。

*  基本类型

    * bool

    * string

    * int、int8、int16、int32、int64。int 在32位系统为32，在64位为64位

    * uint、uint8、unit16、unit32、uint64、uinptr。uint、uintptr 同 int

    * byte，uint8的别名

    * rune，int32的别名，表示一个 Unicode

    * float32、float64

    * complex64、complex128

    * 除非有特殊理由，一般整数值应使用`int`类型

* 没有明确初始值的变量声明会被赋予它们的零值，零值有：

    * 数值类型为0

    * 布尔类型为 `false`

    * 字符串为`""`

* Go 在不同类型的项之间赋值需要显示转换。`T(v)`表示将值`v`转换为类型`T`。例如`var f :=float64(64)`

* 常量不能用`:=`语法声明。`const Pi = 3.14`。



### 变量的声明周期

生命周期是指程序执行过程中变量存在的时间段。包级别的变量的生命周期是全局的。局部变量的生命周期一直存在直到不可访问。



### 包初始化

包的初始化从初始化包级别的变量开始，按照声明顺序初始化。

在每个文件里，当程序启动的时候，init 函数按照它们声明的顺序自动执行。

包的初始化，按照程序中导入的顺序来进行，依赖顺序优先，main 包最后初始化。



### 作用域

声明的作用域是声明在程序文本中出现的区域，它是编译时属性。变量的生命周期是变量在程序执行期间能被程序的其他部分所引用的起止时间，它是运行时属性。

在包级别，声明的顺序和它们的作用域没有关系，所以一个声明可以引用它自己活着跟在它后面的其他声明。

### 常量

常量生成器iota，在常量声明中，iota 从 0 开始取值，逐项加 1.

```go
type Weekday int 
const (
    Sunday Weekday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
)
```

从属类型待定的常量共有 6 种，分别是无类型布尔、无类型整数、无类型文字符号、无类型浮点、无类型复数、无类型字符串。

* Go 只有一种循环结构 `for`循环，花括号是必须的。

```go

    for i:=0; i<10;i++ {

    // do something

    }

    sum := 1

    for sum < 100 {

        //do something

    }

    for { // 无限循环

    }

```

*  `if`语句的表达式也不需要括号，但是花括号是必须的。而且可以在比较表达式前加一个简单的语句 

```go
if v:=100; v>10 {
}
```

* `switch`语句类似`if`，`case`不需要`break`，它只运行指定的`case`，且无需为常量。

```go

switch os:= runtime.GOOS; os {
 case "darwin":
 case "linux" :
 default : 
```

* `switch`的`case`语句按照从上到下顺次执行。直到匹配成功为止。
* 没有条件的`switch` 同`switch true`一样
* `defer`语句会将函数推迟到外层函数返回之后才被调用。 推迟调用的函数其参数会立即求值。
* 推迟的函数调用会被压入一个栈中。当外层函数返回同时，被推迟的函数会按照先进后出的顺序调用。 

### 类型声明

type 声明定义一个新的命名类型，它和某个已有类型使用相同的底层类型。`type name underlying-type` 

对于每个类型 T，都有一个对应的类型转换操作 T(x) 将值转换为类型 T，如果两个类型具有相同的底层类型或者二者都指向相同底层类型变量的未命名指针类型，则二者是可以相互转换的。

命名类型的底层类型决定了它的结构和表达方式，以及它支持的内部操作集合，这些操作与直接使用底层类型的情况相同。

## 基本类型

### 字符串

#### 格式化

| 字符  | 含义                                                  |
| ----- | ----------------------------------------------------- |
| `%t`  | 输出一个布尔值                                        |
| `%T`  | 输出一个值得类型，包括函数签名                        |
| `%x`  | 将一个数组或者 slice 里面的字节按照十六进制的方式输出 |
| `%#v` | 以类似 Go 语法的方式输出对象                          |



##高级类型

### 指针

* `*T`表示指向`T`类型值的指针，其零值为`nil`。

* `&`会生成一个指向其操作数的指针。 Go 没有指针运算

```go

var p *int

i := 42

p = &i 

*p = 21

```



### 结构体

结构体就是一个字段的集合。

```go
type Vertex struct {
    X int 
    Y int
}
v := Vertex{1, 2}
v.X = 4
p := &v // p.Y 其实是(*p).Y的简写。
c := v
p.Y = 1
c.X = 1
```

* 命名结构体类型 `S` 不可以定义一个相同结构体类型 `S` 的成员变量，但是可以定义一个`S`的指针类型 `*S`。

* 成员变量的顺序对结构体同一性很重要，顺序不一样视为不同的结构体类型。
* 结构体的零值由结构体成员的零值组成。
* 没有任何成员变量的结构体称为空结构体，写作`struct{}` 。它没有长度，不携带任何信息。例如当做 map 的值类型，来表示只有键是有用的。

#### 结构体字面量

```go
type Point struct{X, Y int}

p := Point{1,2} //按照正确的顺序为每个成员赋值
p1:= Point{X:1} // 指定成员变量的名称和值来初始化，未指定的成员为零值
```

​	通常结构体使用指针的方式使用。

```go
pp := &Point{1, 2} 
//等价于
pp := new(Point)
*pp = Point{1, 2}
```

#### 结构体的比较

​	如果结构体的所有成员变量都可以比较，那么这个结构体就是可以比较的。因此可比较的结构体可以作为 map 的键类型。

#### 结构体嵌套和匿名成员

```go
type Point struct {
  X, Y int
}

type Circle struct {
  Point
  Radius int
}

type Wheel struct {
  Circle
  Spokes int
}
var w Whell 
w.X = 8 // 等价于 w.Circle.Point.X = 8

w = Wheel{Circle{Point{8, 8}, 5}, 20} // 结构体字面量没有快捷方式来初始化结构体
w1 = Wheel {
  Circle : Circle {
    Point: Point{X:8, Y:8},
    Radius: 5,
  },
  Spokes: 20,
}
```

​	匿名成员的可导性由它们的类型决定的，即使这两个结构体不可导出(`point`、`circle`)，仍然可以使用快捷方式 `w.X=8`，但是不能在包外使用 `w.circle.point.X = 8`。

### 数组

数组时具有固定长度且拥有零个或多个相同数据类型元素的序列。长度是数组类型的一部分，所以`[3]int` 和`[4]int`是不同的数组类型。数组类型必须是常量表达式。

```go
var a [2]string // 元素为对应类型的零值
primes := [6]int{2,3,4,5,6,7}
var c = [3]int = [3]int{1,2,3} //数组字面量初始化数组
b := [...]string{"P", "T"} // 自动统计数组长度
```

也可以给出对应的索引和索引值，没有指定索引位置的元素赋予零值

```go
type Currency int 
const (
	USD Currency = iota
  RMB
)
symbol :=[...]string{USD: "$", RMB:"￥"}
fmt.Println(RMB, symbol[RMB]) // "1 ￥"

r := [...]int{99:-1} //其余元素都是 0
```

如果数组的元素是可以比较的，那么数组也是可以用`==`比较的，比较的结果是两边元素的值是否完全相同，包括顺序。



### slice

slice 表示一个拥有相同类型元素的可变长度的序列。slice 通常写成 `[]T`，看起来像是没有长度的数组类型。

slice 有三个属性：指针、长度和容量。指针指向数组第一个可以从 slice 中访问的元素，长度值 slice 中元素的个数，容量指从 slice 起始元素到底层数组最后一个元素间元素的个数。`len`、`cap`可以分别返回 slice 的长度和容量。

```go
months := [...]string{1:"January", /*...*/,12: "December"}
summer := months[6:9] // 不包含 9 
fmt.Println(summer[:20]) // 宕机，超过了容量
fmt.Println(summer[:5]) // 扩展了 slice "[June July August September October]"
```

* slice不会创建新的数组，而是原数组的引用。更改slice会导致原数组也更改


* 注意，slice `a[0:len(a)]`、`a[:len(a)]`、`a[0:]`、`a[:]`是等价的。

**slice 的比较**

slice 无法使用`==`做比较，可以使用`bytes.Equal`来比较两个字节 slice([]byte)。

slice 唯一允许的比较操作是 `nil` ，其值为 `nil`的 slice 没有对应的底层数组、长度和容量都是零。反之不成立。

```go
var s []int    // len(s) == 0, s == nil
s = nil        // len(s) == 0, s == nil
s = []int(nil) // len(s) == 0, s == nil
s = []int{}    // len(s) == 0, s != nil
```

所以推荐使用`len(s) ==0 `来检查 slice 是否为空。 另外除非特殊标注，无论值是否为`nil`，Go 函数都应该以相同的方式对待所有长度为零的 slice。

`func make([]T, len, cap) []T`函数会分配一个元素为零值的数组并返回一个引用了它的切片。

```go
make([]int, 5) // len = 5
make([]int, 5, 6) // len = 5 cap = 6
```

#### append 函数

`append`函数用来将元素追加到 slice 后面。

```go
var s []int
s = append(s, 10)
s = append(s, 11, 13, 15)
s = append(s, b...) // b 为另一个切片
```

`append`函数的原理是，如果容量足够则创建一个新的 slice，底层数组不变；如果容量不够，创建一个新的底层数组，并copy 元素到新数组。

此外虽然底层数组的元素是间接引用的，是 slice 的指针、长度、和容量不是，因此只要是有可能改变 slice的长度、容量或是使得 slice 指向不同底层数组的操作，都需要更新 slice。





#### 可能的陷阱

因为切片引用了原始的数组的空间，导致 GC 不能释放数组空间：只用到少数元素却导致整个数组的内容一值保存在内存里。解决方法就是将感兴趣的数据复制到一个新的切片中。

字符串子串操作和堆字节 slice ([]byte)做 slice 操作的区别：如果 x 是字符串，那么`x[m:n]`返回的是一个字符串，反之返回的是自己 slice



### map

map 是无序键值对的集合，其中`k` 必须是可以通过 `==`来进行比较的数据类型。

```go
args := make(map[string]int) // 创建一个从 string 到 int 的 map
args := map[string]int{
  "alice": 31,
  "charlie": 34
}
delete(args, "alice") // 移除元素
```

新的空 map 的另外一种表达式是`map[string]int{}` 

无法获取 map 元素的地址，一个原因是 map 的增长导致已有元素被重新散列到新的存储位置，这样导致获取的地址无效。

map 的零值是`nil`，大多数操作可以安全的在 map 的零值上执行，包括查找元素、删除元素、`len(map)`、执行`range`循环，这和空 map 行为一致，但是向零值 map 设置元素回导致错误。

键不在 map 中，将得到 map 值类型的零值，但是如何辨别出一个不存在的元素或者恰好是 0 的元素，可以这样做

```go
if age, ok := ages["bob"]; !ok {
  /* ....*/
}
```

### JSON

`json.Marshal`可将 Go 对象序列化为 json 字符串，`json.MarshalIdent`可以输出整齐格式化过的结果，这个函数有两个参数，第一个参数定义每行输出的前缀字符串，另外一个定义缩进的字符串。

只有可导出的成员可以转换为JSON 字段，另外`Year`对应的转换为`released`，`omitempty`的含义表示`Color`是零值或者为空时，不输出这个成员到 JSON 中。

```go
type Movie struct {
  Title string
  Year int `json:"released"`
  Color bool `json:"color,omitempty"`
  Actors []string
}
var movies = []Movie{
	{Title: "Casablanca", Year: 1942, Color: false,
		Actors: []string{"Humphrey Bogart", "Ingrid Bergman"}},
	{Title: "Cool Hand Luke", Year: 1967, Color: true,
		Actors: []string{"Paul Newman"}},
	{Title: "Bullitt", Year: 1968, Color: true,
		Actors: []string{"Steve McQueen", "Jacqueline Bisset"}},
	// ...
}

data, err := json.Marshal(movies)
if err != nil {
	log.Fatalf("JSON marshaling failed: %s", err)
}
fmt.Printf("%s\n", data)

data, err := json.MarshalIndent(movies, "", "    ")
```

​	`unmarshal` 将 JSON 字符串反序列化成 Go 对象。

```go
var titles []struct{ Title string }

if err := json.Unmarshal(data, &titles); err != nil{
  log.Fatalf("JSON unmarshaling failed: %s", err)
}
fmt.Println(titles)
```

`json.newDecoder(io.Reader).Decoder` 流式解码器，依次从字节流里面解码出多个 JSON 实体。同样，也有`json.newEncoder(io.Writer).Encoder`流式编码器。

### 文本和 HTML 模板

​	模板可以将格式和代码分离，模板是一个字符串或者文件，包含多个用`{{}}` 包围起来的操作。操作可以输出值、选择结构体成员、调用函数和方法、描述控制逻辑、实例化其他模板等。这些都通过`text/template`、`html/template`包里面的方法实现。

```go
const templ = `{{.TotalCount}} issues:
{{range .Items}}----------------------------------------
Number: {{.Number}}
User:   {{.User.Login}}
Title:  {{.Title | printf "%.64s"}}
Age:    {{.CreatedAt | daysAgo}} days
{{end}}`

```

​	`.TotalCount`中的 `.`表示模板里面的参数，`.Number`中的`.`表示`Items`里面连续的元素。`{{range .Items}}` 、`{{end}}`表示创建一个循环。 `|`会将前一个操作的结构当做下一个操作的输入。`printf`是内置函数，`fmt.Sprintf`的同义词。

​	通过模板输出结果需要两步

	1. 解析模板并转换为内部的表示方法
 	2. 在指定的输入上面执行

```go
report, err := template.New("report").
		Funcs(template.FuncMap{"daysAgo": daysAgo}).
		Parse(templ)
	if err != nil {
		log.Fatal(err)
	}
// 或者使用 template.Must
var report = template.Must(template.New("issuelist").
	Funcs(template.FuncMap{"daysAgo": daysAgo}).
	Parse(templ))

if err := report.Execute(os.Stdout, result); err != nil {
		log.Fatal(err)
	}
```

​	`template.Must`提供了一种便捷的处理错误方式，接受模板和 `err`，如果`err!=nil` 则宕机，然后返回这个模板。

`html/template`同`text/template` 有同样的 API，但会对字符串进行转义，防止注入攻击。

我们可以使用`template.CSS`、`template.JS`、`template.URL` 、`template.HTML`来处理受信任的 CSS、JavaScript、URL、HTML 文本。





### 函数值

* 函数也是值，也可以像其他值一样传递，可以用作函数的参数以及返回值。

```go

func compute(fn func(float64, float64) float64) float64 {
    return fn(3, 4)
}
func main() {
    hypot := func(x, y float64) float64 {
        return math.Sqrt(x*x + y*y)
    }
    fmt.Println(hypot(5, 12))
    fmt.Println(compute(hypot))
    fmt.Println(compute(math.Pow))
}

```

* 函数可以是一个闭包。引用其函数体之外的变量。该函数可以访问并赋予其引用的变量的值，换句话说，该函数被 “绑定” 在了这些变量上。例如，函数 adder 返回一个闭包。每个闭包都被绑定在其各自的 sum 变量上。

* 注意闭包没有方法名

```go

func adder() func(int) int {
    sum := 0
    return func(x int) int {
        sum += x
        return sum
    }
}
func main() {
    pos, neg := adder(), adder()
    for i := 0; i < 10; i++ {
        fmt.Println(
            pos(i),
            neg(-2*i),
        )
    }
}

```

##函数

### 函数声明

每个函数声明包含一个名字、形参列表、可选的返回列表以及函数体

```go
func name(parameter-list)(result-list){
  body
}
```

当只有一个返回值或者没有返回值时，返回列表的括号可以省略。

多个形参或者返回值的类型相同，可以只需写一次。

```go
func f(i, j, k int, s, t string){}
```

函数的类型称为函数签名，拥有相同形参列表和返回列表的函数的类型或签名是相同的。

Go 没有默认参数值的概念，也不能指定实参名。

函数形参和命名返回值都属于函数最外层的作用域的局部变量。

实参是按值传递的，所以函数接收到的是每个实参的副本，修改形参变量不会影响到实参，包括对象、数组等。如果提供的实参包含引用类型，比如指针、slice、map、函数或者通道，那么函数就有可能间接的修改实参变量。

有些函数的声明没有函数体，那说明这个函数使用了 Go 以为的语言实现。

函数如果有命名的返回值，则可以省略`return`语句的操作数，这称为裸返回。但不推荐这么做，不便于理解。

### 错误

当函数调用发生错误时返回一个附加的结果作为错误值，习惯上将错误作为最后一个结果返回。如果错误只有一种情况，通常设置为布尔类型。更多的时候，返回 `error`类型的结果。

当函数返回一个非空错误时，其他结果都是未定义且应该忽略的。

#### 处理错误策略

1. 将错误传递下去，使用`fmt.Errorf` 格式化一条错误消息并且返回一个新的错误值。设计一个错误消息应当谨慎，确保每一条错误消息都是有意义的，包含充足的相关信息，并且保持一致。
2. 重试若干次数，超过之后再报错退出。
3. 输出错误，然后调用`os.Exit(1)`优雅的停止程序。
4. 记录错误信息，然后继续运行程序
5. 直接忽略

### 函数变量

函数可以赋给变量、传递或者从其他函数中返回。函数签名不同的变量不可赋值。函数可以和 `nil`比较，但是本身不可比较。

### 匿名函数

命名函数只能在包级别的作用域进行声明，函数字面量可在任何表达式内指定函数变量。

通过函数字面量定义的函数能够取到整个词法环境，里层的函数可以使用外层函数的变量。

```go
func squares() func() int {
  var x int 
  return func() int {
    x++
    return x*x
  }
}
```

#### 陷进：捕获迭代变量

```go
var rmdirs []func()
for _, d := range tempDirs() {
  dir := d  // ①
  os.MkdirAll(dir, 0755)
  rmdirs = append(rmdirs, func(){
    os.RemoveAll(dir)
  })
}
for _, rmdir := range rmdirs {
  rmdir() //清理
}
```

`d`变量的值在不断迭代中更新，因此当调用清理函数的时候，假如没有①这一步的话，所有的`os.RemoveAll`调用最终都试图删除同一目录，最后一次迭代时的目录。

### 变长函数

在参数列表最后的类型名称之前使用省略号，表示声明一个变长函数，调用时可以传递任意数目的参数。

```go
func sum(vals ...int) int {
  total := 0
  for _, val := range vals {
    total += val
  }
  return total
}
fmt.Println(sum())
fmt.Println(sum(3))
fmt.Println(sum(2,3,4))

values := []int{1,2,3,4,5}
fmt.Println(sum(values...))
```

`interface{}` 类型意味着函数可以接受任何值。

### 延迟函数调用

`defer` 语句修饰的函数调用，会推迟到包含`defer`语句的函数执行完毕后才执行，不论函数是正常执行完毕，还是异常退出。`defer` 语句没有限制使用次数，执行的时候以调用`defer`语句顺序的倒序进行。 

`defer`一般用于释放资源，正确使用`defer`语句的地方是成功获得资源之后。

```go
f, err := os.Open(filename)
if err != nil {
  return nil, err
}
defer f.Close()
return ReadAll(f)
```

`defer`也可用于在函数入口、出口处设置调试行为

```go
func bigSlowOperation() {
	defer trace("bigSlowOperation")() // don't forget the extra parentheses

	time.Sleep(10 * time.Second) 
}

func trace(msg string) func() {
	start := time.Now()
	log.Printf("enter %s", msg)
	return func() { log.Printf("exit %s (%s)", msg, time.Since(start)) }
}
```

`defer`执行的函数在`return`语句之后，因此可以打印返回的结果，甚至修改返回结果的值。

### panic 和 recover

Go 语言在运行时检测到一些错误会发生宕机，例如数组越界。一个典型的宕机发生时，正常的程序执行会终止，goroutine 中的所有延迟函数会执行，然后程序会异常退出并留下一条日志消息。

`panic` 是内置的宕机函数，可以接受任值作为参数。可以使用该函数来处理不可能发生的错误。

`runtime`包提供了转储栈的方式，使程序员可以诊断错误。

```go
func main() {
	defer printStack()
	f(3)
}
func printStack() {
	var buf [4096]byte
	n := runtime.Stack(buf[:], false)
	os.Stdout.Write(buf[:n])
}
func f(x int) {
	fmt.Printf("f(%d)\n", x+0/x) // panics if x == 0
	defer fmt.Printf("defer %d\n", x)
	f(x - 1)
}
```

退出程序通常是正确处理宕机的方式，但也有例外，例如 web 程序。 

如果内置的`recover` 函数在延迟函数的内部调用，并且这个包含`defer`语句的函数发生宕机，`recover`会终止当前宕机状态，并且返回宕机的值。函数不会继续运行而是正常返回。

从同一个包内发生的宕机进行恢复有助于简化处理复杂和未知的错误，但一般的原则是，不应该尝试恢复从另一个包内发生的宕机，尤其是第三方API 的宕机，因为你不知道这样做是否安全。

有些情况下是没有恢复动作的，例如内存耗尽使得 Go 运行时发生严重错误。

## 方法

在 Go 中方法和函数是有区别的。方法是指和某个类型绑定的函数。因此方法的声明和函数类型，只是前面多了一个参数，要绑定的类型。方法和字段使用同一个命名空间，不可重名。

```go
type Point struct{ X, Y float64}

func (p Point) Distance(q Point) float64{
  return math.Hypot(q.X - p.X, q.Y-P.Y)  
}
```

附加的参数 `p`成为方法的接受者。表示主调方法就像向对象发送消息。

Go 可以将方法绑定到任何类型上，包括Go 本身内置的简单类型。 

### 指针接受者的方法

由于主调函数会复制每一个实参变量，如果函数需要更新一个变量，或者实参太大希望避免复制整个实参，因此我们必须使用指针来传递变量的地址。这也适用于更新接受者。

```go
func (p *Point) ScaleBy(factor float64){
  p.X *= factor
  P.Y *= factor
}
```

习惯上，如果一个类型的任何一个方法使用指针接受者，那么该类型的所有方法都应该使用指针接受者，即时有些方法不一定需要。

**合法的方法调用**

1. 实参接收者和形参接受者是同一类型，都是`T`类型或者`*T`类型。
2. 实参接收者是`T`类型，而形参接受者是`*T`类型，编译器或隐式的获取变量的地址
3. 实参接收者是`*T`类型，而形参接受者是`T`类型，编译器或隐式地解引用接受者，获取实际取值。获取不到是不允许的。

nil 是一个合法的接受者

### 结构体内嵌

内嵌使得一个结构体包含另外一个结构体的所有字段，这条规则也同样适用于方法。

结构体内嵌看来像是面向对象语言的继承。但是实质上，内嵌更像是编译器生成额外的包装方法来调用内嵌结构体声明的方法。 

```go
type ColoredPoint struct {
  Point
  Color color.RGBA
}

// 实质上相当于以下代码
func (p ColoredPoint)Distance(q Point) float64 {
  return p.Point.Distance(q)
}
```

编译器处理选择方法时，首先查找直接声明的方法、之后从内嵌字段的方法中查找、再之后从内嵌的内嵌字段的方法查找，以此类推。当同一个查找级别中有同名方法时，会报错。

### 方法变量与方法表达式

```go
p := Point{1, 2}
q := Point{4, 6}
distanceFromP := p.Distance // 方法变量
fmt.Println(distanceFromP(q))

distance := Point.Distance // 方法表达式
fmt.Println(distance(p, q))
```



## 接口

* 接口类型是由一组方法签名定义的集合。接口类型变量可以保存任何实现这些方法的值。

* 类型通过实现一个接口的所有方法来实现该接口。

```go
type I interface {
    M()
    L()
}
type T struct {
    S string
}
// 此方法表示类型 T 实现了接口 I，但我们无需显式声明此事。
func (t *T) M() {
    fmt.Println(t.S)
    t.S = "M"
}
func (t *T) L() {
    fmt.Println("L = " + t.S)
}
func main() {
    i:= T{"hello"}
    i.M()
    i.L()
}
```

* 在内部，接口值可以看做包含值和具体类型的元组。接口值保存了一个具体类型的具体值。接口调用方法时会执行其底层的同名方法。

* 即便接口内的具体值为`nil`，方法依然会被`nil`接受者调用不会触发空指针异常。

```go

func main() {
    var i I
    var t *T
    i = t
     fmt.Printf("(%v, %T)\n", i, i) //(<nil>, *main.T)

    i.M()  //<nil>

    i = &T{"hello"}
    describe(i)
    i.M()
}

```

* 接口的具体值和具体类型都为`nil`的话，调用方法会抛出异常。

* 指定零个方法的接口值被称为空接口，空接口可保存任何类型的值。

* 类型断言提供了访问接口值底层具体值的方式。 `t := i.(T)

```go

var i interface{} = "hello"
    s := i.(string)
    fmt.Println(s)
    s, ok := i.(string)
    fmt.Println(s, ok)
    f, ok := i.(float64)  // f为零值，ok 为 false 表示断言失败，不会引发异常
    fmt.Println(f, ok) 
    f = i.(float64) // panic  该语句会引发异常
    fmt.Println(f)

```

* 类型选择，`v`为接口值。

```go

    switch v := i.(type) {
    case int:
        fmt.Printf("Twice %v is %v\n", v, v*2)
    case string:
        fmt.Printf("%q is %v bytes long\n", v, len(v))
    default:
        fmt.Printf("I don't know about type %T!\n", v)
    }
```

## 错误



## I/O

为了区别文件结束和其他错误操作，`io`包下有个不同的错误——`io.EOF`。

**注意** 很多文件系统中，写错误往往不会立即返回，而是推迟到文件管理的时候，如果不检查关闭操作的结果，就会导致一系列的数据丢失。

## 线程

* `go f(x, y, z)` 会启动一个新的 Go 程并执行，f、x 、y、z 的求值会在当前 Go 程中，而 f 的执行发生在新的 Go 程中。

* 信道是带有类型的管道，你可以通过它用信道操作符 <- 来发送或者接收值。

```go

ch <- v // 将 v 发送至信道 ch。
v := <-ch // 从 ch 接收值并赋予 v。

```

* 信道使用前必须创建，`ch := make(chan int)`
* 信道两端未准备好之前是阻塞的，可设置信道的缓冲，缓冲区填满后才会阻塞。缓冲区为空时，接收方会阻塞。

