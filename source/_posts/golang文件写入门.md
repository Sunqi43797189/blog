---
title: golang文件写入门
date: 2020-04-04 14:43:12
tags: 
  - Golang
categories:
  - Golang  
---

- ioutil
- os.OpenFile 记得写完内容后 file.Sync()
- bufio.NewWriter 写完内容后 writer.Flush()

<!-- more -->

```go
const (
	// O_RDONLY, O_WRONLY, or O_RDWR 必须指定
	O_RDONLY int = syscall.O_RDONLY // 只读
	O_WRONLY int = syscall.O_WRONLY // 只写
	O_RDWR   int = syscall.O_RDWR   // 读写
	// The remaining values may be or'ed in to control behavior.
	O_APPEND int = syscall.O_APPEND // 追加
	O_CREATE int = syscall.O_CREAT  // 如果文件不存在，创建
	O_EXCL   int = syscall.O_EXCL   // 和O_CREATE一起使用, 只有当文件不存在时才创建
	O_SYNC   int = syscall.O_SYNC   // 以同步I/O方式打开文件，直接写入硬盘
	O_TRUNC  int = syscall.O_TRUNC  // 清空文件
)
```

```go
package main

import (
	"bufio"
	"fmt"
	"io/ioutil"
	"os"
)

func main()  {
	// writeFileIoUtil()
	// wirteFileOsOpenFile()
	writeFileBufio()
}

// writeFileIoUtil 覆盖式写入,不会自动写入换行
func writeFileIoUtil() {
	c := "content"
	c1 := "content1"
	data := []byte(c)
	data1 := []byte(c1)
	ioutil.WriteFile("./1.txt", data, 0644)
	ioutil.WriteFile("./1.txt", data1, 0644)
}

// 不会自动写入换行
func wirteFileOsOpenFile() {
	file, err := os.OpenFile("./1.txt", os.O_CREATE | os.O_RDWR | os.O_APPEND, 0644)
	if err != nil {
		fmt.Printf("file open err %v", err)
	}
	defer file.Close()
	c := []byte("hello world\n")
	if n, err := file.Write(c); err != nil {
		fmt.Printf("file write err %v", err)
	} else {
		fmt.Println(n)
	}
	c1 := "wakakawakaka\n"
	if n, err := file.WriteString(c1); err != nil {
		fmt.Printf("file write err %v", err)
	} else {
		fmt.Println(n)
	}
	file.Sync()
}

func writeFileBufio() {
	file, err := os.OpenFile("./1.txt", os.O_CREATE | os.O_RDWR | os.O_APPEND, 0644)
	if err != nil {
		fmt.Printf("file open err %v", err)
	}
	defer file.Close()
	writer := bufio.NewWriter(file)
	c := []byte("hello world\n")
	n, err := writer.Write(c)
	if err != nil {
		fmt.Printf("file write err %v", err)
	}
	fmt.Println(n)
	s := "wakakawakaka\n"
	n, err = writer.WriteString(s)
	if err != nil {
		fmt.Printf("file write err %v", err)
	}
	fmt.Println(n)
	writer.Flush()
}
```
