---
title: golang异常
date: 2020-04-06 22:37:12
tags:
	- Golang
categories:
	- Golang	
---
- 自定义错误
- panic宕机
- recover 捕获宕机错误

<!-- more-->

1. 自定义错误, 结构体实现 Error 接口
```go
    func New(text string) error {
      return &errorString{text}
    }
    type errorString struct {
      s string
    }
    func (e *errorString)Error() string {
      return e.s
    }
```
2. panic 宕机，宕机后的所有语句不会执行，但是会执行宕机前的defer语句，recover 捕获宕机错误
```go
    package main
    import "fmt"
    func main() {
      defer fmt.Println("1111")
      defer func()  {
        err := recover()
        fmt.Println("err is ", err)
      }()
      panic("panic")
    }
```
3. 发生异常时函数获取返回值,主函数callFunc没有指定返回值的变量时无法获取返回值内容
```go
    package main

    import "fmt"

    func callPanic() (a int) {
        defer fmt.Println("1111")
        defer func() {
            if info := recover(); info != nil {
                a = 1
            } else {
                a = 2
            }
        }()
        panic("panic")
    }

    func main() {
        fmt.Println(callPanic())
    }
```