---
title: GolangBenchMark测试
date: 2020-06-01 18:44:09
tags:
  - Golang
categories: 
  - Golang
---

### 要求：

- 文件名以`_test.go`结尾

- 测试函数名必须以`Benchmark`开头

- 必须重写`Repeat`函数

- 运行次数不用自己指定，系统自动决定

- 运行命令 `go test -bench=. -run=none`

### 示例：

```go
func BenchmarkMatch(b *testing.B) {
    ac := ahocorasick.NewMatcher()
    client := redis.NewClient(&redis.Options{
        Addr:     "localhost:6379",
        DB:       0,
    })
    dictionary := client.ZRange(context.Background(), "moment_sensitive_words", 0, -1).Val()
    ac.Build(dictionary)
    for i := 0; i < b.N; i++ {
        Repeat(ac)
    }
}
func Repeat(ac *ahocorasick.Matcher) {
    ret := ac.Match("阿不都热合曼")
    if len(ret) != 0 {
        _ = ret[0]
    }
}
```

{% asset_img benchmark.png image %}

1. 核心数

2. 运行次数

3. 每次耗费时间
