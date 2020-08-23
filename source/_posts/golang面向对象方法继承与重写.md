---
title: golang面向对象方法继承与重写
date: 2020-04-17 17:30:06
tags:
  - Golang
categories:
  - Golang
---

### 继承

> Go语言中可以创建一个或者多个类型作为嵌入字段的自定义结构体，任何嵌入类型中的方法都可以当作该自定义结构体自身的方法被调用，从而间接实现子类继承父类的方式

### 重写

> 子类定义了与父类同名的方法

<!--more-->

```go
package main

import "fmt"

type Person struct {
	name string
	age int
}

type Employee struct {
	Person
	salary int
}

func (p Person) sayName()  {
	fmt.Printf("p:name: %s\n", p.name)
}

func (p Person) sayAge() {
	fmt.Printf("p:age: %d\n", p.age)
}

func (e Employee) sayAge() {
	fmt.Printf("e:age: %d\n", e.age)
}

func main()  {
	p := Person{age: 1, name: "tom"}
	e := Employee{Person: p, salary: 100}
	e.sayName() // 继承
	p.sayAge()
	e.sayAge() // 方法重写
	e.Person.sayAge() // 子类调用父类被重写的方法
}
```



