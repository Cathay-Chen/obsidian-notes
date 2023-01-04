## 开发环境
## 基础语法
## 语法特性

### defer
defer 是 Go 语言中的关键字，也是 Go 语言的重要特性之一，defer 在资源释放、panic 捕获等场景中的应用非常广泛。

```go
defer func(...){
	// 实际处理
}()
```

我们需要掌握 defer 的几个重要特性，包括：
#todo
- 延迟执行；
- 参数预计算 [[Go defer 参数预计算]]；
- LIFO（后进先出）执行顺序。

Go语言的defer关键字的执行顺序是LIFO（后进先出）。下面是一个示例：

```go
package main

import "fmt"

func main() {
	fmt.Println("Start")
	defer fmt.Println("Deferred 1")
	defer fmt.Println("Deferred 2")
	fmt.Println("End")
	
	// 输出结果为：
	// Start End Deferred 2 Deferred 1
}
```

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