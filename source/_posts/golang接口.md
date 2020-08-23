---
title: golang接口
date: 2020-04-17 16:45:17
tags:
  - Golang
categories:
  - Golang
---

- 实现接口条件
- 实现接口方式
- 空接口

<!--more-->



### 实现接口条件：

- 接口中的方法都被实现

- 方法的参数与返回值与接口中的一样

### 实现接口方式

- 实体类型以值接收者实现接口的时候，不管是实体类型的值，还是实体类型值的指针，都实现了该接口

- 指针类型实现接口，赋值时需要传递地址，因为结构体的指针实现了接口，结构体并没有实现

  ```go
  package main
  import "fmt"
  type animal interface {
    printInfo()
  }
  type cat int
  type dog int
  func (c cat) printInfo(){
    fmt.Println("cat")
  }
  func (d *dog)printInfo() {
    fmt.Println("dog")
  }
  func main() {
    var c cat
    var d dog
    invoke(c)
    invoke(&c)
    invoke(&d)
    //invoke(d) // 报错
  }
  func invoke(a animal) {
    a.printInfo()
  }
  ```

### 空接口

- 空接口获取值

  ```go
  var a int = 1
  var i interface{} = a
  var b int = i.(int) // 类型断言获取值
  ```

- 空接口值的比较 可以直接使用 == 判断

- 空接口中含有动态类型时不能进行比较

  ```go
  var a interface{} = []int{10}
  var b interface{} = []int{20}
  a == b // panic runtime error: comparing uncomparable type []int
  ```

- 空接口类型可比较性

  | 类型    | 说明                                                         |      |
  | ------- | ------------------------------------------------------------ | ---- |
  | map     | 宕机错误，不能比较                                           |      |
  | slice   | 宕机错误，不能比较                                           |      |
  | channel | 可比较，必须由同一个make生成，同一个通道才会是true否则为false |      |
  | array   | 可比较，编译期知道两个数组是否一致                           |      |
  | struct  | 可比较，可以逐个比较结构体的值                               |      |
  | func    | 可比较                                                       |      |