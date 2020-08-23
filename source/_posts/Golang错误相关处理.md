---
title: Golang错误相关处理
date: 2020-06-02 20:11:25
tags:
  - Golang
categories:
  - Golang
---

### 基于字符串的错误

```go
err1 := errors.New("error 1")

err2 := fmt.Errorf("error %d", 2)
```

### 自定义错误

```go
package main

import (
    "errors"
    "fmt"
    "runtime/debug"
)

type BaseError struct {
    InnerError error
    Message    string
    StackTrace string
    Misc       map[string]interface{}
}

func WrapError(err error, message string, messageArgs ...interface{}) BaseError {
    return BaseError{
        InnerError: err,
        Message:    fmt.Sprintf(message, messageArgs),
        StackTrace: string(debug.Stack()),
        Misc:       make(map[string]interface{}),
    }
}

func (err *BaseError) Error() string {
    return err.Message
}

func main() {
    err := WrapError(errors.New("测试error"), "测试message", map[string]string{"name": "sunqi"})
    fmt.Println(err.Error())
}
```
