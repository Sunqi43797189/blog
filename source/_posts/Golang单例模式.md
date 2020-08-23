---
title: Golang单例模式
date: 2020-06-01 18:37:30
tags:
  - Golang
categories:
  - Golang
---

### 传统加锁模式

因为加锁，并发安全，并且不会每次调用都加锁，执行效率高

```go
type singleton struct{}
var ins *singleton
var mu sync.Mutex
func GetIns() *singleton{  
　　if ins == nil {
        mu.Lock()
        defer mu.Unlock()
        if ins == nil {
            ins = &singleton{}
        }
    }
    return ins
}
```

### sync.Once

```go
func GetAc() {
    once.Do(func(){
        ac = ahocorasick.NewMatcher()
        client := redis.NewClient(&redis.Options{
            Addr:     "localhost:6379",
            DB:       0,
        })
        dictionary := client.ZRange(context.Background(), "moment_sensitive_words", 0, -1).Val()
        ac.Build(dictionary)
        fmt.Println("初始化")
    })
}
```
