---
title: 写给前端工程师的Golang入门教程 —— 内置类型
date: 2021-08-25 00:00:00
tags: Golang
---
`JavaScript`是一门弱类型的语言，对于数据类型定义比较宽泛，`Golang`是一门强类型的语言，对于的类型定义比较细致。

### 基本类型

| 类型        | 长度        | 说明 |
| ---        | ---         | --- |
|`bool`      | 1           | 对应JavaScript的Boolean|
|`string`    |             | 对应JavaScript的String|
|`(u)int`    | 4/8         | 32或64位|
|`(u)int8`   | 1           | -128 ~ 127, 0 ~ 255|
|`(u)int16`  | 2           | -32768 ~ 32767, 0 ~ 65535|
|`(u)int32`  | 4           | -2147483648 ~ 2147483647, 0 ~ 4294967295|
|`(u)int64`  | 8           | -9223372036854775808 ~ 9223372036854775807, 0 ~ 18446744073709551615|
|`uintptr`   | 4/8         | 存储指针的uint32或uint64整数|
|`byte`      | 1           | uint8的别名|
|`rune`      | 4           | int32的别名, Unicode码点|
|`float32`   | 4           | 符合IEEE-754标准的32位浮点数 |
|`float64`   | 8           | 符合IEEE-754标准的64位浮点数 |
|`complex64` | 8           | 具有float32实部和虚部的所有复数的集合 |
|`complex128`| 16          | 具有float64实部和虚部的所有复数的集合 |

### 数组

`JavaScript`的数组声明不用关注元素类型和数组长度

```javascript
let a = [1, 2, 3]
```

`Golang`要求声明元素类型和数组长度

```golang
var a = [3]int{1, 2, 3}
```

`Golang`数组长度是声明在类型前面的，并且也可以让编译器计算

```golang
var a = [...]int{1, 2, 3}
```

### 切片

`Golang`的数组声明需要事先定义数组长度，看起来不像`JavaScript`中的数组那么好用，实际上与`JavaScript`中的数组对等的应该是`Golang`的切片。

数组是值类型，切片是在数组上面的一个‘View’，它指向一个数组的一段连续的内存。

初始化一个切片也很简单，直接去掉数组长度的声明就是切片

```golang
var a = []int{1, 2, 3}
```

在切片元素不确定的情况下，我们还可以使用`make`初始化一个切片

```golang
var a = make([]int, 3)
var b = make([]int, 3, 6)
```

>初始化一个长度为3的切片a；初始化一个长度为3，数组的容量为6的b。

`Golang`提供了一些方法操作切片

`len()`可以查看切片的长度
`cap()`可以查看切片指向的数组的长度
>相当于`JavaScript`中的`Array.prototype.length`属性

`append()`可以追加元素到切片中，并且有扩容指向的数组的能力
>相当于`JavaScript`中的`push()`

还可以使用`[low:high]`切片操作
>相当于`JavaScript`中的`Array.prototype.slice()`方法

### Map

Map是一种无序的Key-Value数据结构，相当于`JavaScript`中的`Map`

初始化Map需要声明类型

```golang
var a = map[string]string
var b = map[string]string {
  "foo": "Hello",
  "bar": "World"
}
```

也可以使用`make`

```golang
var a = make(map[string]string)
```

使用`delete()`删除`key`

### 结构体

结构体可以看作是`JavaScript`中的`Object`，不过需要事先定义字段。

```golang
type Person struct {
  name string
  age int
}

var a = Person{name: "allen", age: 30}
var b = Person{"allen", 30}
var c = new(Person)
c.name = "allen"
c.age = 30
```

`new()`是`Golang`的一个内置函数，它会根据传入的类型分配一片内存空间并返回指向这片内存空间的指针。

欢迎关注我的公众号“**野生程序员的修炼**”，原创技术文章第一时间推送。

<center>
    <img src="https://gitee.com/noodanee/resource/raw/master/2021/08/13/1628787241618-a4cdaa95-d14e-4422-8851-f616c8f18f04.jpg" style="width: 100px;">
</center>
