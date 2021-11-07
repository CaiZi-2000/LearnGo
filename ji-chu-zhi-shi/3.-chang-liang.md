# 3. 常量



在 Go 语言中， <mark style="color:blue;">**常量**</mark> 表示的是固定的值，常量表达式的值在编译期进行计算，常量的值不可以修改。例如： `3` 、 `Let's go` 、 `3.14` 等等。常量中的数据类型只可以是 <mark style="color:blue;">**布尔型**</mark> 、 <mark style="color:blue;">**数字型**</mark> （整数型、浮点型和复数）和 <mark style="color:blue;">**字符串型**</mark> 。

### 常量的声明

常量的声明使用关键字 `const` ：

```go
const <name> <type> = <expression>
const <name> = <expression>
```

多个相同类型的声明可以写成：

```go
const <name1>, <name2> = <expression1>, <expression2>
```

下面是一个声明常量的例子：

```go
package main

import "fmt"

func main() {
	const a int = 10
	const b = "Let's go"
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)
	// a = 12 // error
}
```

运行该程序输出如下：

```
a =  10
b =  Let's go
```

因为常量不能修改，如果把最后一行的注释去掉，编译会出错。

下面的例子，因为函数调用发生在运行时，所以不能将函数的返回值赋值给常量。

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var a = math.Abs(-1.2)
	// const b = math.Abs(-3.1)	// error
	fmt.Println(a)
}
```

当然，和变量声明一样，常量也可以一组一起声明，这比较适合声明一组相关的常量：

```go
const (
    e  = 2.71828182845904523536028747135266249775724709369995957496696763
    pi = 3.14159265358979323846264338327950288419716939937510582097494459
)
```

如果是一次声明一组常量，除了第一个外，其它常量右边的初始化表达式都可以省略，如果省略初始化表达式则表示使用前面常量的初始化表达式写法，对应的常量类型也一样的。例如：

```go
package main

import (
	"fmt"
)

const (
	num1 = 1
	num2
	num3 = 2
	num4
)

func main() {
	fmt.Println("num1 = ", num1)
	fmt.Println("num2 = ", num2)
	fmt.Println("num3 = ", num3)
	fmt.Println("num4 = ", num4)
}
```

上面的程序输出为：

```
num1 =  1
num2 =  1
num3 =  2
num4 =  2
```

同样的，一组常量一起声明可以用作枚举：

```go
const (
    Monday = 1
    Tuesday = 2
    Wednesday = 3
    Thursday = 4
    Friday = 5
    Saturday = 6
    Sunday = 7
)
```

当然，后面还有更好的枚举写法。

常量间的所有算术运算、逻辑运算和比较运算的结果也是常量，对常量的类型转换操作或以下函数调用都是返回常量结果： `len()` 、 `cap()` 、 `real()` 、 `imag()` 、 `complex()` 和 `unsafe.Sizeof()` 。注意在常量表达式中，函数必须是内置函数，否则编译不通过。

```go
package main

import (
	"fmt"
	"unsafe"
)

func main() {
	const (
		a = "Let's go"
		length = len(a)
		size = unsafe.Sizeof(a)
	)

	fmt.Println("a = ", a)
	fmt.Println("length = ", length)
	fmt.Println("size = ", size)
}
```

上面程序的输出结果如下：

```
a =  Let's go
length =  8
size =  16
```

当然，你可能对最后一行的输出有些疑惑，为什么 `size` 大小是 `16` ，这里解释一下， `size` 指的是类型的大小，此处为字符串类型大小，字符串类型在 Go 中是一个结构，包含指向底层数组的指针和长度，这两部分每部分都是 `8` 个字节，所以字符串类型大小为 `16` 个字节，所以输出为 `16` 。

### 无类型常量

Go 中的常量有个不同寻常之处。虽然一个常量可以有任意一个确定的基础类型，但是许多常量并没有一个明确的基础类型。这里有六种未明确类型的常量类型，分别是 <mark style="color:blue;">**无类型的布尔型**</mark> 、 <mark style="color:blue;">**无类型的整数**</mark> 、 <mark style="color:blue;">**无类型的字符**</mark> 、 <mark style="color:blue;">**无类型的浮点数**</mark> 、 <mark style="color:blue;">**无类型的复数**</mark> 、 <mark style="color:blue;">**无类型的字符串**</mark> 。

### iota 常量生成器

`iota` 特殊常量，可以认为是一个可以被编译器修改的常量。常量声明可以使用 `iota` 常量生成器初始化，它用于生成一组以相似规则初始化的常量，但是不用每行都写一遍初始化表达式。在一个 `const` 声明语句中，在第一个声明的常量所在的行， `iota` 将会被置为 `0` ，然后在每一个有常量声明的行加一。 `iota` 可以被用作枚举值：

```go
package main

import (
	"fmt"
)

const (
	Sunday int = iota
	Monday
	Tuesday
)

func main() {
	fmt.Println("Sunday = ", Sunday)
	fmt.Println("Monday = ", Monday)
	fmt.Println("Tuesday = ", Tuesday)
}
```

上面的程序输出为：

```
Sunday =  0
Monday =  1
Tuesday =  2
```

如果出现另一个 `const` 声明语句， `iota` 将会重新置为 `0` ：

```go
package main

import (
	"fmt"
)

const (
	a = iota    // iota = 0
	b           // iota = 1
	c           // iota = 2
	d = "go"    // go, iota = 3
	e           // 和上一行一样为 go, iota = 4
	f = 100     // 100, iota = 5
	g           // 和上一行一样为 100, iota = 6
	h = iota    // iota = 7
	i           // iota = 8
)

const (
	j = iota    // iota 重新计数, iota = 0
	k           // iota = 1
)

func main() {
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)
	fmt.Println("c = ", c)
	fmt.Println("d = ", d)
	fmt.Println("e = ", e)
	fmt.Println("f = ", f)
	fmt.Println("g = ", g)
	fmt.Println("h = ", h)
	fmt.Println("i = ", i)
	fmt.Println("j = ", j)
	fmt.Println("k = ", k)
}
```

程序输出如下：

```
a =  0
b =  1
c =  2
d =  go
e =  go
f =  100
g =  100
h =  7
i =  8
j =  0
k =  1
```
