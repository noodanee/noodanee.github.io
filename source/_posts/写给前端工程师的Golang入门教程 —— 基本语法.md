---
title: 写给前端工程师的Golang入门教程 —— 基本语法
date: 2021-08-21 00:00:00
tags: Golang
---
在前端我们主要使用`JavaScript`作为主要开发语言，我们来逐一对比`JavaScript`与`Golang`的语法特性，来帮助前端工程师更快入门`Golang`。

### 变量声明

在`JavaScript`中，使用`var`或`let`关键字来声明变量

```javascript
{
  let a = 10
  var b = 1
}
```

在`Golang`中，同样使用`var`关键字声明变量

```golang
var a = 10
```

由于`Golang`是一门强类型的语言，如果省略了类型声明，编译器会做类型推导，上面这种变量声明方式实际上等价于

```golang
var a int = 10
```

在函数中，使用`:=`符号可以更简便的声明并初始化变量

```golang
func main() {
  a := 10
}
```

除了变量，我们还有声明常量的需求，`Golang`和`JavaScript`常量的声明方式也是一样的

```golang
const a = 10
```

### 条件语句

`JavaScript`的条件分支语法继承自`C`语言

```javascript
let a = 10
if (a > 0) {
  console.log(a)
}
```

`Golang`的条件分支不带小括号，支持在条件里写多个表达式，用`;`号分割，并且在条件里声明的变量只在`if`条件模块内部有效

```golang
if a := 10; a > 0 {
  fmt.Println(a)
}
```

条件分支中最容易忽略的是`switch`结构。

在`JavaScript`中，每个`case`要使用`break`关键字终止流程

```javascript
switch (fruit) {
  case "banana":
    // ...
    break
  case "apple":
    // ...
    break
  default:
    // ...
}
```

`Golang`很人性化，每个`case`会自动`break`

```golang
switch fruit {
  case "banana":
    // ...
  case "apple":
    // ...
  default:
    // ...
}
```
如果需要顺序执行代码，还加`fallthrough`关键字

### 循环语句

在`JavaScript`中，循环语句有`while`、`do while`、`for`、`for in`、`for of`

在`Golang`中，没有那么多花里胡哨的东西，只有万能的`for`

```golang
for i := 0; i < 100; i++ {
  fmt.Println(i)
}
```

`for`的起始条件、递增条件、结束条件都是可选的，甚至可以不带任何条件，就表示一个死循环

```golang
for {
  // ...
}
```

### 函数

在`JavaScript`中，函数用`function`关键字声明

在`Golang`中，函数用`func`关键字声明，并且与`JavaScript`一样，函数是一等公民，支持闭包

```golang
func createIncrementor(start int) func() int {
	return func () int {
	  start++
	  return start;
	}
}
  

func main() {
	inc := createIncrementor(5);
  
	inc() // 5
	inc() // 6
	inc() // 7
}
```


欢迎关注我的公众号“**野生程序员的修炼**”，原创技术文章第一时间推送。

<center>
    <img src="https://gitee.com/noodanee/resource/raw/master/2021/08/13/1628787241618-a4cdaa95-d14e-4422-8851-f616c8f18f04.jpg" style="width: 100px;">
</center>
