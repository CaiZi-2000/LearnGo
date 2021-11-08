# 4. 整型

在 Go 语言中，整型可以细分成两个种类十个类型。

### 有符号整型：

<mark style="color:blue;">**int8**</mark> ：表示 `8` 位有符号整型；其类型宽度为 `8` 位，即 `1` 字节，表示范围： `-128` \~ `127` 。

<mark style="color:blue;">**int16**</mark> ：表示 `16` 位有符号整型；其类型宽度为 `16` 位，即 `2` 字节，表示范围： `-32768` \~ `32767` 。

<mark style="color:blue;">**int32**</mark> ：表示 `32` 位有符号整型；其类型宽度为 `32` 位，即 `4` 字节，表示范围： `-2147483648` \~ `2147483647` 。

<mark style="color:blue;">**int64**</mark> ：表示 `64` 位有符号整型；其类型宽度为 `64` 位，即 `8` 字节，表示范围： `-9223372036854775808` \~ `9223372036854775807` 。

<mark style="color:blue;">**int**</mark> ：根据不同的底层平台(Underlying Platform)，表示 `32` 或 `64` 位整型。除非对整型的大小有特定的需求，否则你通常应该使用 `int` 表示整型。其类型宽度在 `32` 位系统下是 `32` 位，而在 `64` 位系统下是 `64` 位。表示范围：在 `32` 位系统下是 `-2147483648` \~ `2147483647` ，而在 `64` 位系统是 `-9223372036854775808` \~ `9223372036854775807` 。

```go
package main

import (
	"fmt"
	"math"
	"unsafe"
)

func main() {
	var num8 int8 = 127
	var num16 int16 = 32767
	var num32 int32 = math.MaxInt32
	var num64 int64 = math.MaxInt64
	var num int = math.MaxInt
	fmt.Printf("type of num8 is %T, size of num8 is %d, num8 = %d\n",
		num8, unsafe.Sizeof(num8), num8)
	fmt.Printf("type of num16 is %T, size of num16 is %d, num16 = %d\n",
		num16, unsafe.Sizeof(num16), num16)
	fmt.Printf("type of num32 is %T, size of num32 is %d, num32 = %d\n",
		num32, unsafe.Sizeof(num32), num32)
	fmt.Printf("type of num64 is %T, size of num64 is %d, num64 = %d\n",
		num64, unsafe.Sizeof(num64), num64)
	fmt.Printf("type of num is %T, size of num is %d, num = %d\n",
		num, unsafe.Sizeof(num), num)
}
```

其中，程序中的 `Printf` 方法，可以使用 `%T` 格式说明符(Format Specifier)打印出变量的类型。而 `unsafe` 包的 `Sizeof` 函数接收变量并返回它的字节大小。使用 `unsafe` 包可能会带来可移植性问题，这里只是作为演示使用。如果你将 `num8` 的值改为 `128` 运行后就会报错，因为 `int8` 类型的最大值为 `127` 。该程序运行后输出如下：

```
type of num8 is int8, size of num8 is 1, num8 = 127
type of num16 is int16, size of num16 is 2, num16 = 32767
type of num32 is int32, size of num32 is 4, num32 = 2147483647
type of num64 is int64, size of num64 is 8, num64 = 9223372036854775807
type of num is int, size of num is 8, num = 9223372036854775807
```

### 无符号整型：

<mark style="color:blue;">**uint8**</mark> ：表示 `8` 位无符号整型；其类型宽度为 `8` 位，即 `1` 字节，表示范围： `0` \~ `255` 。

<mark style="color:blue;">**uint16**</mark> ：表示 `16` 位无符号整型；其类型宽度为 `16` 位，即 `2` 字节，表示范围： `0` \~ `65535` 。

<mark style="color:blue;">**uint32**</mark> ：表示 `32` 位无符号整型；其类型宽度为 `32` 位，即 `4` 字节，表示范围： `0` \~ `4294967295` 。

<mark style="color:blue;">**uint64**</mark> ：表示 `64` 位无符号整型；其类型宽度为 `64` 位，即 `8` 字节，表示范围： `0` \~ `18446744073709551615` 。

<mark style="color:blue;">**uint**</mark> ：根据不同的底层平台，表示 `32` 或 `64` 位无符号整型。其类型宽度在 `32` 位系统下是 `32` 位，而在 `64` 位系统下是 `64` 位。表示范围在 `32` 位系统下是 `0` \~ `4294967295` ，而在 `64` 位系统是 `0` \~ `18446744073709551615` 。

```go
package main

import (
	"fmt"
	"math"
	"unsafe"
)

func main() {
	var num8 uint8 = 128
	var num16 uint16 = 32768
	var num32 uint32 = math.MaxUint32
	var num64 uint64 = math.MaxUint64
	var num uint = math.MaxUint
	fmt.Printf("type of num8 is %T, size of num8 is %d, num8 = %d\n",
		num8, unsafe.Sizeof(num8), num8)
	fmt.Printf("type of num16 is %T, size of num16 is %d, num16 = %d\n",
		num16, unsafe.Sizeof(num16), num16)
	fmt.Printf("type of num32 is %T, size of num32 is %d, num32 = %d\n",
		num32, unsafe.Sizeof(num32), num32)
	fmt.Printf("type of num64 is %T, size of num64 is %d, num64 = %d\n",
		num64, unsafe.Sizeof(num64), num64)
	fmt.Printf("type of num is %T, size of num is %d, num = %d\n",
		num, unsafe.Sizeof(num), num)
}
```

该程序运行结果如下：

```
type of num8 is uint8, size of num8 is 1, num8 = 128
type of num16 is uint16, size of num16 is 2, num16 = 32768
type of num32 is uint32, size of num32 is 4, num32 = 4294967295
type of num64 is uint64, size of num64 is 8, num64 = 18446744073709551615
type of num is uint, size of num is 8, num = 18446744073709551615
```

`uint` 无符号整型和 `int` 有符号整型的区别就在于一个 `u` ，有 `u` 的就表示无符号，没有 `u` 的就表示有符号。

接下来讲讲它们表示范围的差别，例如 `int8` 和 `uint8` ，它们的类型宽度都为 `8` 位，能表示的数值个数为 $$2^{8} = 256$$ ，对于无符号整数来说，表示的都是正数，所以表示范围为 `0` \~ `255` ，一共 `256` 个数。而对于有符号整数来说，就得借一位来表示符号，所以表示范围为 `-128` \~ `127` ，刚好也是 `256` 个数。

对于 `int8` ， `int16` 等这些类型后面有跟一个数值的类型来说，它们能表示的数值个数是固定的。而对于 `int` ， `uint` 这两个没有指定其大小的类型，在 `32` 位系统和 `64` 位系统下的大小是不同的。所以，在有的时候例如在二进制传输、读写文件的结构描述(为了保持文件的结构不会受到不同编译目标平台字节长度的影响)等情况下，使用更加精确的 `int32` 和 `int64` 是更好的。

### 不同进制的表示方法

一般我们习惯使用十进制表示法，当然，有时候我们也会使用其他进制表示一个整数。在 Go 中，以 `0b` 或 `0B` 开头的数表示 <mark style="color:blue;">**二进制**</mark> ，以 `0o` 或 `0O` 开头的数表示 <mark style="color:blue;">**八进制**</mark> ，以 `0x` 或 `0X` 开头的数表示 <mark style="color:blue;">**十六进制**</mark> 。

```go
package main

import (
	"fmt"
)

func main() {
	var num2 int = 0b1100011
	var num8 int = 0o143
	var num10 int = 99
	var num16 int = 0X63
	fmt.Println("num2 = ", num2)
	fmt.Println("num8 = ", num8)
	fmt.Println("num10 = ", num10)
	fmt.Println("num16 = ", num16)
}
```

该程序的四个数都表示十进制的 `99` ，程序运行后输出如下：

```
num2 =  99
num8 =  99
num10 =  99
num16 =  99
```

当然，你也可以使用 `fmt` 包的格式化输出相应的进制数。

```go
package main

import (
	"fmt"
)

func main() {
	var num2 int = 0b1100011
	var num8 int = 0o143
	var num10 int = 99
	var num16 int = 0X63
	fmt.Printf("2进制数   num2 = %b\n", num2)
	fmt.Printf("8进制数   num8 = %o\n", num8)
	fmt.Printf("10进制数  num10 = %d\n", num10)
	fmt.Printf("16进制数  num16 = %x\n", num16)
}
```

该程序运行后输出如下：

```
2进制数   num2 = 1100011
8进制数   num8 = 143
10进制数  num10 = 99
16进制数  num16 = 63
```
