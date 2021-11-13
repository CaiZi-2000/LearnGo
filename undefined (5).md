# 5. 浮点型

Go 语言提供了两种精度的浮点数： <mark style="color:blue;">**float32**</mark> <mark style="color:blue;"></mark>和 <mark style="color:blue;">**float64**</mark> ，它们的算术规范由 IEEE754 浮点数国际标准定义。

浮点数类型的值一般由 `整数` 部分、小数点 `.` 和 `小数` 部分组成。其中，整数部分和小数部分均由十进制表示法表示。

不过还可以用科学计数法表示。指数部分由 `E` 或 `e` 以及一个带正负号的十进制数组成。例如 `6.2E-2` 表示浮点数 `0.062` ， `6.2E+1` 表示浮点数 `62` 。

有时候，浮点数类型值的表示也可以被简化。例如， `66.0` 可以被简化为 `66` 。又比如， `0.066` 可以被简化为 `.066` 。

```go
package main

import (
	"fmt"
)

func main() {
	var num1 = 6.2E-2
	var num2 = 6.2E+1
	var num3 float64 = 66
	var num4 float64 = .066
	fmt.Printf("type of num1 is %T, num1 = %f\n", num1, num1)
	fmt.Printf("type of num2 is %T, num2 = %f\n", num2, num2)
	fmt.Printf("type of num3 is %T, num3 = %f\n", num3, num3)
	fmt.Printf("type of num4 is %T, num4 = %f\n", num4, num4)
}
```

该程序运行后输出如下：

```
type of num1 is float64, num1 = 0.062000
type of num2 is float64, num2 = 62.000000
type of num3 is float64, num3 = 66.000000
type of num4 is float64, num4 = 0.066000
```

<mark style="color:blue;">**float32**</mark> ：即常说的单精度，存储占用 `4` 个字节，即 `32` 位，其中 `1` 位用来表示符号， `8` 位用来表示指数，剩下的 `23` 位用来表示尾数。

<mark style="color:blue;">**float64**</mark> <mark style="color:blue;"></mark>：即常说的双精度，存储占用 `8` 个字节，即 `64` 位，其中 `1` 位用来表示符号， `11` 位用来表示指数，剩下的 `52` 位用来表示尾数。

精度主要取决于尾数部分的位数。

对于 `float32` (单精度)来说，表示尾数部分为 `23` 位，除去全部为 `0` 的情况以外，最小为 $$2^{-23}$$ ，约为 $$1.19 * 10^{-7}$$ ，所以 `float32` 小数部分能精确到后面 `6` 位，加上小数点前的一位，即有效数字为 `7` 位。

对于 `float64` (双精度)来说，表示尾数部分为 `52` 位，最小为 $$2^{-52}$$ ，约为 $$2.22 * 10^{-16}$$ ，所以 `float64` 小数部分能精确到后面 `15` 位，加上小数点前的一位，有效位数为 `16` 位。

常量 `math.MaxFloat32` 表示 `float32` 能取到的最大数值，大约是 `3.4e38` ； `float32` 能表示的最小值近似为 `1.4e-45` 。

常量 `math.MaxFloat64` 表示 `float64` 能取到的最大数值，大约是 `1.8e308` ； `float64` 能表示的最小值近似为 `4.9e-324` 。

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	var num1 float32= math.MaxFloat32
	var num2 float64 = math.MaxFloat64
	fmt.Printf("type of num1 is %T, num1 = %g\n", num1, num1)
	fmt.Printf("type of num2 is %T, num2 = %g\n", num2, num2)
}
```

该程序运行后输出如下：

```
type of num1 is float32, num1 = 3.4028235e+38
type of num2 is float64, num2 = 1.7976931348623157e+308
```

通过上面的程序，我们知道浮点数能表示的数值很大，但是浮点数的精度却没有那么大。

`float32` 的精度只能提供大约 `6` 个十进制数(表示后科学计数法后，小数点后 `6` 位)的精度。

`float64` 的精度能提供大约 `15` 个十进制数(表示后科学计数法后，小数点后 `15` 位)的精度。

例如 `10000011` 这个数，用 `float32` 的类型来表示的话，由于其有效位是 `7` 位，将 `10000011` 表示成科学计数法，就是 $$1.0000011 * 10^{7}$$ ，能精确到小数点后面 `6` 位。此时用科学计数法表示后，小数点后有 `7` 位，刚刚满足我们的精度要求，对这个数进行 `+1` 或者 `-1` 等数学运算，都能保证计算结果是精确的。

```go
package main

import (
	"fmt"
)

func main() {
	var num float32= 10000011
	fmt.Printf("type of num is %T\n", num)
	fmt.Printf("num = %g\n", num)
	fmt.Printf("num + 1 = %g\n", num + 1)
}
```

该程序运行后输出结果如下：

```
type of num is float32
num = 1.0000011e+07
num + 1 = 1.0000012e+07
```

可以看到结果精确，没有错误。接下来对这个数进行修改，扩展一位，即 `100000111` 用 `float32` 的类型来表示，对这个数进行 `+1` 运算，看看这里的结果是否正确。

```go
package main

import (
	"fmt"
)

func main() {
	var num float32= 100000111
	fmt.Printf("type of num is %T\n", num)
	fmt.Printf("num = %f\n", num)
	fmt.Printf("num + 1 = %f\n", num + 1)
	fmt.Println(num == num + 1)
}
```

该程序运行后输出结果如下：

```
type of num is float32
num = 100000112.000000
num + 1 = 100000112.000000
true
```

你会发现，结果居然一样！而且 `num == num + 1` 居然为 `true` 。这也正是由于其类型是 `float32` 精度不足，导致产生的结果不精确。

在 `math` 包中除了提供大量常用的数学函数外，还提供了 IEEE754 浮点数标准中定义的特殊值的创建和测试： `正无穷大` 和 `负无穷大` ，分别用于表示太大溢出的数字和除零的结果；还有 `NaN` 非数，一般用于表示无效的除法操作结果 `0/0` 或 `Sqrt(-1)` 。

```go
package main

import (
	"fmt"
)

func main() {
	var num float64
	fmt.Printf("num = %f\n", num)
	fmt.Printf("-num = %f\n", -num)
	fmt.Printf("1/num = %f\n", 1/num)
	fmt.Printf("-1/num = %f\n", -1/num)
	fmt.Printf("num/num = %f\n", num/num)
}
```

该程序运行后输出如下：

```
num = 0.000000
-num = -0.000000
1/num = +Inf
-1/num = -Inf
num/num = NaN
```

函数 `math.IsNaN` 用于测试一个数是否为非数 `NaN` ， `math.NaN` 则返回非数对应的值。虽然可以用 `math.NaN` 来表示一个非法的结果，但是测试一个结果是否是非数 `NaN` 则是充满风险的，因为 `NaN` 和任何数都是不相等的，因为在浮点数中， `NaN` 、 `正无穷大` 和 `负无穷大` 都不是唯一的，每个都有非常多种的 `bit` 模式表示：

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	nan := math.NaN()
	fmt.Println("nan == nan ? ", nan == nan)
	fmt.Println("nan < nan ? ", nan < nan)
	fmt.Println("nan > nan ? ", nan > nan)
}
```

所以，该程序运行后输出结果都为 `false` ：

```
nan == nan ?  false
nan < nan ?  false
nan > nan ?  false
```
