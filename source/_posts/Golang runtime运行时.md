---
title: golang runtime运行时
date: 2020-04-18 11:12:28
tags:
  - Golang
categories:
  - Golang
---

- **Gosched**：让当前线程让出 `cpu` 以让其它线程运行,它不会挂起当前线程，因此当前线程未来会继续执行
- **NumCPU**：返回当前系统的 `CPU` 核数量
- **GOMAXPROCS**：设置最大的可同时使用的 `CPU` 核数
- **Goexit**：退出当前 `goroutine`(但是`defer`语句会照常执行)
- **NumGoroutine**：返回正在执行和排队的任务总数
- **GOOS**：目标操作系统

<!--more-->

### NumCPU NumGoroutine GOOS

```go
func runtimeInfo()  {
    runtime.GOMAXPROCS(1)
    fmt.Println(runtime.NumCPU()) // 返回当前cpu核心数
    fmt.Println(runtime.NumGoroutine()) // 返回正在执行和排队的任务数
    fmt.Println(runtime.GOOS) // 返回当前操作系统
}
```

### Gosched

```go
func runtimeGosched()  {
    go func (s string)  {
        for i := 0; i < 4; i ++{
            fmt.Println(s)
        }
    }("world")

    for i := 0; i < 4; i ++{
        runtime.Gosched()
        fmt.Println("hello")
    }
}
```

### Goexit

```go
func runtimeGoexit()  {
    go func ()  {
        fmt.Println(111)
        defer fmt.Println("A defer")
        func ()  {
            defer fmt.Println("B.defer")
            runtime.Goexit()
            defer fmt.Println("C.defer")
            fmt.Println("B")
        }()
        fmt.Println("A")
    }()
    for{
    }
}
```
