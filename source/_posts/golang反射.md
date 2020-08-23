---
title: golang反射
date: 2020-05-06 11:12:00
tags:
  - Golang
categories:
  - Golang

---

1. 反射 `reflect.TypeOf()`，返回输入参数接口中的值的类型对象，如果为空则返回nil

2. 反射 `reflect.ValueOf()`，返回输入参数接口中的数据的值对象，如果为空返回0

3. `Kind()` 种类

4. `Name()` 类型名称
   
   ```go
   func testReflect(){
       var name string = "tom"
       reflectType := reflect.TypeOf(name)
       reflectValue := reflect.ValueOf(name)
       fmt.Println(reflectType, reflectValue) // string, 'tom'
     fmt.Println(reflectType.Kind()) // string
     fmt.Prin tln(reflectType.Name()) // string
   }
   ```
