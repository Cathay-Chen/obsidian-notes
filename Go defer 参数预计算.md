在使用 `defer` 语句时，会先对参数进行预计算，然后延迟执行函数。

例如，在下面的代码中，我们使用 `defer` 关键字延迟调用 `fmt.Println` 函数：

```go
package main

import "fmt"

func main() {
    i := 1
    defer fmt.Println(i)
    i++
    fmt.Println("Hello, world!")
}

```

在这段代码中，变量 `i` 的值是 1，但是因为 `defer` 语句在函数返回之前倒序执行，所以 `fmt.Println(i)` 会在最后输出，输出的值是 2。

所以，输出的结果是：

```
Hello, world!
2
```

注意，如果 `defer` 语句中的函数需要传入参数，那么这些参数会在 `defer` 语句执行时进行预计算，而不是在延迟执行函数时计算。

所以，在上面的代码中，参数 `i` 的值是在 `defer` 语句执行时计算的，而不是在 `fmt.Println` 函数调用时计算。