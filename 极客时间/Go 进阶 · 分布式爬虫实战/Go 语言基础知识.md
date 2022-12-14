## 开发环境
1. 安装语言处理系统（从而能够解释、编译或运行编写的代码）。
2. 配置好 Go 语言的环境变量，包括 GOPATH、GOPROXY。
3. 搭建好舒适的集成开发环境（GoLand、Vim、VSCode 或者 Emacs），以便快速开发代码。
4. 合格的开发者需要熟悉编辑器中的快捷键，例如上移 (Up)、下移 (Down)、右移 (Right)、左移 (Left)、复制当前或选中行（Duplicate Line or Selection）、提取选中内容为函数（Extract Method)，还有众多的快捷键我在这里就不赘述了。[[Goland 快捷键]]
5. 掌握 Go 的一些命令行工具，特别是一些基础的命令。只要在命令行中执行 Go，就有多种子命令可供选择。这些命令及其含义如下：
| Command     | 说明                               |
| ----------- | ---------------------------------- |
| go bug      | 打开浏览器，报告错误信息           |
| go build    | 编译源代码                         |
| go clean    | 移除目标文件和缓存文件             |
| go env      | 打印 Go 环境信息                   |
| go fix      | 旧版本代码修正为新版本             |
| go fmt      | 格式化源文件                       |
| go generate | 扫描特殊注释，用于自动生成 Go 文件 |
| go get      | 添加指定版本依赖                   |
| go list     | 列出指定代码包的信息               |
| go mod      | 依赖管理工具                       |
| go run      | 编译并运行源代码                   |
| go test     | 测试代码                           |
| go tool     | 运行热书的 Go 工具                 |
| go version  | 打印 Go 版本                       |
| go vet      | 静态扫描代码，报告代码中可能的错误 | 

## 基础语法

Go 中要掌握的基础语法和其他的高级语言是类似的。它包括了变量与类型、表达式与运算符、基本控制结构、函数和复合类型。

### 变量与类型

#### 变量的声明与赋值

示例：

```go
  // 使用var关键字声明变量并指定类型
  var x int
  
  // 为变量赋值
  x = 5
  
  // 还可以同时声明和赋值
  var y float32 = 7.5
  
  // 如果未指定类型，Go 将推断变量的类型
  z := "hello"
}

```

#### Go 中的内置类型

- `bool`：值为 `true` 和 `false` 的布尔类型
- `string`：用于存储和操作文本的字符串类型
- `int`、`int8`、`int16`、`int32` 和 `int64`：具有不同大小的有符号整数类型
- `uint`、`uint8`、`uint16`、`uint32`、`uint64` 和 `uintptr`: 具有不同大小的无符号整数类型
- `byte`：`uint8` 的别名
- `rune` ：`int32` 的别名，表示 Unicode 代码点
- `float32` 和 `float64`：具有不同大小的浮点类型
- `complex64` 和 `complex128` ：带浮点实部和虚部的复数
	
#### 变量的命名规则

1. 变量名由字母、数字和下划线组成，但不能以数字开头。
2. 区分大小写，因此在 Go 语言中大写字母开头的变量名是公共的（public），小写字母开头的变量名是私有的（private）。
3. 不能使用 Go 语言的保留字作为变量名。

> 建议使用驼峰命名法来命名变量，这样的命名方式更加规范和易读。例如，可以使用 `userName` 来命名变量，而不是 `username` 或 `user_name`。
	
```go
// 合法的变量名
var userName string
var user_name string

// 不合法的变量名
var 123user string   // 不能以数字开头
var user-name string // 不能包含特殊字符
var break string     // 不能使用 Go 保留字
```

#### 变量的生命周期

变量的生命周期可以通过变量的作用域来确定。在 Go 语言中，变量的作用域可以是包级别的（package-level）或者是函数内部的（function-level）。

包级别的变量在整个包中都是可见的，函数内部的变量仅在函数内部是可见的。变量的生命周期是指变量存在的时间段。包级别的变量的生命周期是整个程序的生命周期，函数内部的变量的生命周期是在函数被调用时开始，在函数执行完毕后结束。

例如：

在下面的示例中，`packageLevelVariable` 的生命周期是整个程序的生命周期，而 `functionLevelVariable` 的生命周期只在 `main` 函数被调用时存在。

```go
// 包级别的变量
var packageLevelVariable int

func main() {
    // 函数内部的变量
    var functionLevelVariable int
}
```


#### 变量的作用域

Go 的词法范围使用花括号{…}作为分割。根据作用域的范围大小，可以分为全局作用域、包作用域、文件作用域、函数作用域。

### 表达式与运算符

除了需要对变量有深入理解外，你还需要掌握表达式与运算符，帮助程序完成基础的运算。运算符包括：
- 算术运算符；
- 关系运算符；
- 逻辑运算符；
- 位运算符；
- 赋值运算符；
- 地址运算符。

当这些运算符同时存在时，还需要考虑运算符优先级的顺序：

| 优先级 (由高到低) | 操作符                 | 
| ---------------- | ---------------------- | 
| 5                | *  /  %  <<  >>  &  &^ | 
| 4                | +  -  \|  ^            | 
| 3                | ==  !=  <  <=  >  >=   |
| 2                | &&                     |
| 1                | \|\|                    |   

### 基本控制结构

#### if else 语句

```go
if condition {
	// run code
} else if condition {
	// run code
} else {
	// run code
}
```

#### switch 语句

```go
switch var1 {
    case val1:
        //...
    case val2, val3:
        //...
    default:
        //...
}
```

#### for 循环语句

1. 完整的 C 风格的 for 循环

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

2. 只有条件判断的 for 循环

```go
i := 1
for i < 100 {
        fmt.Println(i)
        i = i * 2
}
```

3. 无限循环的 for 循环

```go
func main() {
    for {
        fmt.Println("Hello")
    }
}
```

4. for-range 循环

```go
evenVals := []int{2, 4, 6, 8, 10, 12}
for i, v := range evenVals {
    fmt.Println(i, v)
}
```

### 函数

#### 基本用法

- 基础函数声明

```go
func name(parameter-list) (result-list) {
    body
}
```

- 函数的多返回值特性 ：

```go
func div (a, b int) (int, error) {
    if b == 0 {
	    return 0, errors.New("b cat't be 0")
    }
    return a/b,nil
}
```

- 可变参数函数

```go
func Println(a ...interface{}) (n int, err error)
```

#### 函数作为一等公民拥有一些灵活的特性

- 函数作为参数时，可以提升程序的扩展性

```go
package main
import (
    "fmt"
)
// 遍历切片的每个元素, 通过给定函数进行元素访问
func visit(list []int, f func(int)) {
    for _, v := range list {
        f(v)
    }
}

func main() {
    // 使用匿名函数打印切片内容
    visit([]int{1, 2, 3, 4}, func(v int) {
        fmt.Println(v)
    })
}
```

- 函数作为返回值时，一般在闭包和构建功能中间件时使用得比较多，在不修改过去核心代码的基础上，用比较小的代价增加了新的功能。

```go
func logging(f http.HandlerFunc) http.HandlerFunc{
  return func(w http.ResponseWriter, r *http.Request) {
    log.Println(r.URL.Path)
    f(w,r)
  }
}
```

- 函数作为值时，可以用来提升服务的扩展性

```go
var opMap = map[string]func(int, int) int{
    "+": add,
    "-": sub,
    "*": mul,
    "/": div,
}

f := opMap[op]
f()
```

> 注意，Go 函数调用时参数是值传递，在调用过程中修改函数参数不会影响到原始的值。
> 但是！**在 Go 语言中，指针、切片、字典（map）、接口、函数以及通道（channel）都是引用类型。因此在传递这些类型的参数时，传递的是参数的指针，而不是参数的副本。这意味着，在函数内部对这些类型的参数的修改会影响到原来的参数。** 其他类型的参数，如数组、布尔值、数字、字符串等都是值类型，在传递时都是值传递。

### 复合类型

函数是对功能的抽象，那么复合类型带来了数据的抽象。
Go 语言中内置的复合类型包括：数组、切片、哈希表，以及用户自定义的结构体。

#### 切片

- 声明和赋值

```go
var slice1 []int
numbers:= []int{1, 2, 3, 4, 5, 6, 7, 8}
var x = []int{1, 5: 4, 6, 10: 100, 15}
```

- 使用 append 往切片中添加元素

```go
y := []int{20, 30, 40}
x = append(x, y...)
```

- 切片的截取

```go
numbers:= []int{1, 2, 3, 4, 5, 6, 7, 8}
// 从下标2 一直到下标4，但是不包括下标4
numbers1 :=numbers[2:4]
// 从下标0 一直到下标3，但是不包括下标3
numbers2 :=numbers[:3]
// 从下标3 一直到结尾
numbers3 :=numbers[3:]
```

#### Map 哈希表

- 声明与初始化

```go
var hash map[T]T
var hash = make(map[T]T, NUMBER)
var country = map[string]string{
	"China": "Beijing",
	"Japan": "Tokyo",
	"India": "New Delhi",
	"France": "Paris",
	"Italy": "Rome",
}
```

- 俩种访问方式

```go
v := hash[key]
v,ok := hash[key]
```

- 赋值与删除

```go
m := map[string]int{
    "hello": 5,
    "world": 10,
}
delete(m, "hello")
```


#### 结构体

- 声明与赋值

```go
type Nat struct {
    n  int
    d  int
}
var nat Nat
nat := Nat{
    2,
    3
}
nat.n = 4
natq := Nat{
    d:  3,
    n:  2,
}
```

- 匿名结构体

```go
var person struct {
    name string
    age  int
    pet  string
}

pet := struct {
    name string
    kind string
}{
    name: "Fido",
    kind: "dog",
}
```



### 变量的可比较性

| 类型 | 可比较性 | 说明 |
| ---- | ------ | ---- |
| 布尔 | 可比较 | -      |
| 整数 | 可比较 | -      |
| 浮点 | 可比较 | -      |
| 复数 | 可比较 | -      |
| 字符串 | 可比较 | -      |
| 指针 | 可比较 |如果两个指针指向相同的变量，或者两个指针均为 nil，则它们相等。      |
| 通道 | 可比较 |如果两个通道有相同的 make 函数调用创建的，或者两个通道都为 nil，则它们相等。      |
| 接口 | 可比较 |如果两个接口具有相同的动态类型和相同的动态值，或者两个接口都为 nil，则它们相等。|
| 结构体 | 可比较 |如果结构体所的所有的字段都是可比较的，则它们值是可比较的。      |
| 数组 | 可比较 |如果数组元素的类型可比较，则数组可比较。如果两个数组对应的元素都相等，则它们相等。      |
| 切片 | 不可比较 | -      |
| 函数 | 不可比较 | -      |
| 哈希表 | 不可比较 | -      |


## 语法特性

### defer

defer 是 Go 语言中的关键字，也是 Go 语言的重要特性之一，defer 在资源释放、panic 捕获等场景中的应用非常广泛。

```go
defer func(...) {
	// 实际处理
}()
```

我们需要掌握 defer 的几个重要特性，包括：
- 延迟执行；
- [[Go defer#参数预计算|参数预计算]]；
- [[Go defer#LIFO（后进先出）执行顺序|LIFO（后进先出）执行顺序]]。

除此之外，Go 语言用于异常恢复的内置 recover 函数，也需要与 defer 函数结合使用才有意义：

```go
func f() {
    defer func() {  
	   if r := recover(); r != nil {  
	      fmt.Println("Recovered in f", r)  
	   }  
	}()  
	fmt.Println("Calling g.")  
	panic("panic err")  
	fmt.Println("Returned normally from g.")

	// 输出结果为：
	// Calling g.
	// Recovered in f panic err
}
```

### 接口

- 声明和定义

```go
type Shape interface {
  perimeter() float64
  area() float64
}

var s Shape
```

- 隐式地让一个类型实现接口

```go
type Rectangle struct {
  a, b float64
}

func (r Rectangle) perimeter() float64 {
  return (r.a + r.b) * 2
}

func (r Rectangle) area() float64 {
  return r.a * r.b
}
```

- 接口的动态调用方式

```go
var s Shape
s = Rectangle{3, 4}
s.perimeter()
s.area()
```

- 接口的嵌套

```go
type ReadWriter interface {
  Reader
  Writer
}

type Reader interface {
  Read(p []byte) (n int, err error)
}

type Writer interface {
  Write(p []byte) (n int, err error)
}
```

- 接口类型断言

```go
func main(){
  var s Shape
  s = Rectangle{3, 4}
  rect := s.(Rectangle)
  fmt.Printf("长方形周长:%v, 面积:%v \\n",rect.perimeter(),rect.area())
}
```

- 根据空接口中动态类型的差异选择不同的处理方式（这在参数为空接口函数的内部处理中使用广泛，例如 fmt 库、JSON 库）

```go
switch f := arg.(type) {
  case bool:
    p.fmtBool(f, verb)
  case float32:
    p.fmtFloat(float64(f), 32, verb)
  case float64:
    p.fmtFloat(f, 64, verb)
```


### 协程
### 通道


## 并发编程
## 项目组织
## 工具与库