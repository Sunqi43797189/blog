---
title: Golang定时器
date: 2020-06-15 22:02:00
tags: 
  - Golang
cargeories: 
  - Golang
---



### 另起一个goroutine运行定时器

```go
go func() {
		tk := time.NewTicker(3 * time.Hour)
		for {
			select {
			case <-tk.C:
				initDictionary()
				initMatcher()
				log.Println("3小时更新 ahocorasick")
			}
		}
	}()
```


