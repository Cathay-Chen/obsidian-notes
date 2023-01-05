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

需要掌握的内容如下：

- 变量的声明与赋值。

```go
  // Declare a variable with the var keyword and specify a type
  var x int
  
  // Assign a value to the variable
  x = 5
  
  // You can also declare and assign a value at the same time
  var y float32 = 7.5
  
  // Go will infer the type of the variable if it is not specified
  z := "hello"
}

```


- Go 中的内置类型。



- 



## 语法特性

### defer

defer 是 Go 语言中的关键字，也是 Go 语言的重要特性之一，defer 在资源释放、panic 捕获等场景中的应用非常广泛。

```go
defer func(...){
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

接口、协程、通道


## 并发编程
## 项目组织
## 工具与库