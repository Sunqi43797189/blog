---
title: gin 设置cookie
date: 2020-04-02 23:29:06
tags: 
  - Golang
  - Gin
categories:
  - Golang  
---

最近学习Gin框架，不知道为什么框架的setCookie方法不能用，于是用net/http设置cookie

<!-- more -->

```go
package main
import (
    "fmt"
    "github.com/gin-gonic/gin"
    "net/http"
    "strconv"
)
func main() {
    r := gin.Default()
    r.Use(cookieCheck())
    r.GET("/http_cookie", func(c *gin.Context) {
        if cookie, err := c.Request.Cookie("cookie"); err == nil {
            c.String(http.StatusOK, cookie.Value)
        }
    })
    r.Run(":8080")
}
func cookieCheck() gin.HandlerFunc {
    return func(c *gin.Context) {
        if cookie, err := c.Request.Cookie("cookie"); err == nil {
            value := cookie.Value
            if v, err := strconv.Atoi(value); err == nil {
                i := v + 1
                cookie.Value = fmt.Sprintf("%d", i)
            }
            http.SetCookie(c.Writer, cookie)
            c.Next()
        } else {
            cookie := &http.Cookie{
                Name:  "cookie",
                Value: "0",
            }
            http.SetCookie(c.Writer, cookie)
        }
    }
}
```
