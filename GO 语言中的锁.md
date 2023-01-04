Go 语言提供了若干种锁机制来帮助程序员控制并发：

-   互斥锁 (`sync.Mutex`)
-   读写锁 (`sync.RWMutex`)
-   原子操作 (`sync/atomic` 包)
-   自旋锁 (`sync.SpinLock`)
-   递归锁 (`sync.Mutex` 的 `Lock()` 和 `Unlock()` 函数支持递归调用)

简单来说，互斥锁 (`sync.Mutex`) 和读写锁 (`sync.RWMutex`) 适用于需要完全排他性的场合，而原子操作 (`sync/atomic`) 则更适用于只需要短暂排他性的场合。自旋锁 (`sync.SpinLock`) 适用于排他性不需要太久，但又不能使用原子操作的场合。

注意：原子操作可以避免阻塞，但在多处理器系统上会使得其它的处理器被挂起，因此只适用于需要短暂排他性的场合。

在选择锁的时候，需要根据具体情况进行选择。通常来说，如果代码中有大量的读操作，可以使用读写锁 (`sync.RWMutex`)，否则可以使用互斥锁 (`sync.Mutex`)。


下面是 Go 语言中几种常用锁的用法示例：

互斥锁 (`sync.Mutex`)：

互斥锁 (`sync.Mutex`) 是最基本的锁类型，它能够保证在任意时刻，只有一个 goroutine 能够访问需要保护的代码块。当一个 goroutine 获取互斥锁之后，其它 goroutine 就必须等待直到该 goroutine 释放锁之后才能继续执行。互斥锁适用于需要完全排他性的场合。

示例：

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

读写锁 (`sync.RWMutex`) 是一种特殊的锁类型，它能够同时支持多个读操作和单个写操作。当有多个 goroutine 同时执行读操作时，它们可以并发执行；但是，当有一个 goroutine 执行写操作时，其它的 goroutine 就必须等待直到该 goroutine 完成写操作之后才能继续执行。读写锁适用于有大量的读操作和少量的写操作的场合。

示例：

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

原子性操作 (atomic operation) 指的是在并发环境下执行的一组操作，这组操作要么全部执行，要么全部不执行，不会出现执行一半的情况。原子性操作可以帮助我们保证在并发环境下对共享变量的操作的安全性。

示例：

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

自旋锁 (`sync.SpinLock`) 是一种特殊的锁，它不会使程序阻塞，而是在获取锁失败时，让当前的 goroutine 自旋 (即循环等待) 直到获取到锁为止。自旋锁的优点在于能够保证响应速度，但缺点在于当竞争激烈时可能会导致 CPU 资源的浪费。因此，自旋锁适用于排他性不需要太久，但又不能使用原子操作的场合。

示例：

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

递归锁 (recursive lock) 是指在已经获取到锁的情况下，在同一个 goroutine 中可以再次调用该锁的 `Lock()` 函数，并能够成功获取锁。在 Go 语言中，`sync.Mutex` 的 `Lock()` 和 `Unlock()` 函数支持递归调用，可以用来实现递归锁。

示例：

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