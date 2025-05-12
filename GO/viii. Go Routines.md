# Go Routines 

## What are Goroutines?

Goroutines are lightweight threads managed by the Go runtime. They allow you to perform concurrent tasks in a simple and efficient manner.

* Initiated with the `go` keyword.
* Much more memory-efficient compared to traditional threads.
* Ideal for I/O-bound or high-concurrency applications.

### Syntax

```go
func someFunction() {
    // do something
}

func main() {
    go someFunction() // this runs concurrently
    // main function continues executing
}
```

---

## Key Characteristics

* **Concurrency**: Goroutines allow multiple functions to run independently.
* **Lightweight**: Only a few KBs of stack space; scales easily to millions of goroutines.
* **Managed by Go Scheduler**: Goroutines are multiplexed onto fewer OS threads.

---

## Example: Concurrent Function Execution

```go
package main

import (
    "fmt"
    "time"
)

func say(s string) {
    for i := 0; i < 3; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s)
    }
}

func main() {
    go say("world")
    say("hello")
}
```

**Output:**

```
hello
world
world
hello
hello
```

(Note: Output order may vary due to concurrency.)

---

## Using Anonymous Goroutines

```go
func main() {
    go func(msg string) {
        fmt.Println(msg)
    }("Hello from anonymous goroutine")
    time.Sleep(time.Second)
}
```

---

## Synchronization: WaitGroup

Use `sync.WaitGroup` to wait for a collection of goroutines to finish executing.

```go
package main

import (
    "fmt"
    "sync"
)

func worker(id int, wg *sync.WaitGroup) {
    fmt.Printf("Worker %d starting\n", id)
    // simulate work
    fmt.Printf("Worker %d done\n", id)
    wg.Done()
}

func main() {
    var wg sync.WaitGroup

    for i := 1; i <= 3; i++ {
        wg.Add(1)
        go worker(i, &wg)
    }

    wg.Wait()
    fmt.Println("All workers done")
}
```

---

## Best Practices

* Avoid blocking goroutines indefinitely.
* Use channels and context for communication and cancellation.
* Monitor goroutine leaks in long-running applications.

---

## Debugging Tip

Use the `runtime` or `pprof` package to monitor goroutine count:

```go
fmt.Println("Number of goroutines:", runtime.NumGoroutine())
```

---

