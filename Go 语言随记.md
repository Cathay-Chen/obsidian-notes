 ---
##  ParseInt
```go
// 参数1 数字的字符串形式  
// 参数2 数字字符串的进制 比如二进制 八进制 十进制 十六进制  
// 参数3 返回结果的 bit 大小也就是 int8 int16 int32 int64
func ParseInt (s string, base int, bitSize int) (i int64, err error)  
```

---
## 升级 go 
```shell
brew update
brew upgrade go
```

---
## base64

 [base64 编解码](http://zh.wikipedia.org/wiki/Base64)
```go
data := "abc123!?$*&()'-=@~"

// Go 同时支持标准 base64 以及 URL 兼容 base64。 
// 这是使用标准编码器进行编码的方法。 
// 编码器需要一个 `[]byte`，因此我们将 string 转换为该类型。
sEnc := b64.StdEncoding.EncodeToString([]byte(data))
fmt.Println(sEnc) // YWJjMTIzIT8kKiYoKSctPUB+

// 解码可能会返回错误，
// 如果不确定输入信息格式是否正确， 
// 那么，你就需要进行错误检查了。
sDec, _ := b64.StdEncoding.DecodeString(sEnc)
fmt.Println(string(sDec)) // abc123!?$*&()'-=@~
fmt.Println()

// 使用 URL base64 格式进行编解码。
uEnc := b64.URLEncoding.EncodeToString([]byte(data))
fmt.Println(uEnc) // YWJjMTIzIT8kKiYoKSctPUB-
uDec, _ := b64.URLEncoding.DecodeString(uEnc)
fmt.Println(string(uDec)) // abc123!?$*&()'-=@~
```

---
Urlencode
[How to perform URL decoding in Golang](https://www.urldecoder.io/golang/)

```go
fmt.Println(url.QueryEscape(query))

params := url.Values{}
params.Add("name", "@Rajeev")
params.Add("phone", "+919999999999")

fmt.Println(params.Encode())

path := "path with?reserved+characters"
fmt.Println(url.PathEscape(path))
```

---

## 简单的 Http 服务代码

```go
func startHttp(port int) {  
   port1 := strconv.Itoa(port)  
   if port1 == "" {  
      common.Error("web端口错误")  
      return  
   }  
  
   http.HandleFunc("/healthcheck", func(writer http.ResponseWriter, request *http.Request) {  
      writer.Header().Set("Content-Type", "application/json")  
      writer.WriteHeader(200)  
      encoder := json.NewEncoder(writer)  
      var response struct {  
         State uint        `json:"state"`  
         Data  interface{} `json:"data"`  
         Msg   string      `json:"msg"`  
      }  
      response.State = 200  
      response.Msg = "success"  
  
      if err := encoder.Encode(response); err != nil {  
         http.Error(writer, err.Error(), 500)  
      }  
   })  
  
   common.Info("http listen start", port1)  
  
   if err := http.ListenAndServe(":"+port1, nil); err != nil {  
      common.Error("http listen err", err)  
   }  
}
```


## GO 语言中的锁

Go 语言提供了若干种锁机制来帮助程序员控制并发：

-   互斥锁 (`sync.Mutex`)
-   读写锁 (`sync.RWMutex`)
-   原子操作 (`sync/atomic` 包)
-   自旋锁 (`sync.SpinLock`)
-   递归锁 (`sync.Mutex` 的 `Lock()` 和 `Unlock()` 函数支持递归调用)

简单来说，互斥锁 (`sync.Mutex`) 和读写锁 (`sync.RWMutex`) 适用于需要完全排他性的场合，而原子操作 (`sync/atomic`) 则更适用于只需要短暂排他性的场合。自旋锁 (`sync.SpinLock`) 适用于排他性不需要太久，但又不能使用原子操作的场合。

自旋锁 (`sync.SpinLock`) 是一种特殊的锁，它不会使程序阻塞，而是在获取锁失败时，让当前的 goroutine 自旋 (即循环等待) 直到获取到锁为止。自旋锁的优点在于能够保证响应速度，但缺点在于当竞争激烈时可能会导致 CPU 资源的浪费。因此，自旋锁适用于排他性不需要太久，但又不能使用原子操作的场合。

递归锁 (recursive lock) 是指在已经获取到锁的情况下，在同一个 goroutine 中可以再次调用该锁的 `Lock()` 函数，并能够成功获取锁。在 Go 语言中，`sync.Mutex` 的 `Lock()` 和 `Unlock()` 函数支持递归调用，可以用来实现递归锁。

注意：原子操作可以避免阻塞，但在多处理器系统上会使得其它的处理器被挂起，因此只适用于需要短暂排他性的场合。

在选择锁的时候，需要根据具体情况进行选择。通常来说，如果代码中有大量的读操作，可以使用读写锁 (`sync.RWMutex`)，否则可以使用互斥锁 (`sync.Mutex`)。

下面是 Go 语言中几种常用锁的用法示例：

互斥锁 (`sync.Mutex`)：

```go
import "sync"

var mu sync.Mutex

func main() {
    mu.Lock()
    // 在这里进行需要保护的操作
    mu.Unlock()
}

```

读写锁 (`sync.RWMutex`)：

```go
import "sync"

var rwMu sync.RWMutex

func main() {
    rwMu.RLock()
    // 在这里进行只读操作
    rwMu.RUnlock()

    rwMu.Lock()
    // 在这里进行写操作
    rwMu.Unlock()
}

```

原子操作 (`sync/atomic`)：

```go
import "sync/atomic"

var count int64

func main() {
    atomic.AddInt64(&count, 1)
    atomic.LoadInt64(&count)
    atomic.StoreInt64(&count, 10)
    atomic.SwapInt64(&count, 20)
}

```

自旋锁 (`sync.SpinLock`)：

```go
import "sync"

var spinLock sync.SpinLock

func main() {
    spinLock.Lock()
    // 在这里进行需要保护的操作
    spinLock.Unlock()
}

```

递归锁 (`sync.Mutex` 的 `Lock()` 和 `Unlock()` 函数支持递归调用)：

```go
import "sync"

var mu sync.Mutex

func main() {
    mu.Lock()
    // 在这里进行需要保护的操作
    mu.Unlock()
}
```

注意：在使用锁的时候，一定要保证在调用 `Unlock()` 函数之前必须先调用 `Lock()` 函数。否则会导致程序异常。