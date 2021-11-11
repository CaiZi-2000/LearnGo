# 8. 复数

在 Go 语言中提供了两种精度的 <mark style="color:blue;">**复数**</mark> 类型： <mark style="color:blue;">**complex64**</mark> 和 <mark style="color:blue;">**complex128**</mark> ，分别对应 float32 和 float64 两种浮点数精度。内置的 <mark style="color:blue;">**complex**</mark> 函数用于构建复数，内建的 <mark style="color:blue;">**real**</mark> 和 <mark style="color:blue;">**imag**</mark> 函数分别返回复数的实部和虚部：

```go
package main

import "fmt"

func main() {
	var x complex64 = complex(1, 2)
	var y complex128 = complex(3, 4)
	var z complex128 = complex(5, 6)
	fmt.Println("x = ", x)
	fmt.Println("y = ", y)
	fmt.Println("z = ", z)
	fmt.Println("real(x) = ", real(x))
	fmt.Println("imag(x) = ", imag(x))
	fmt.Println("y * z = ", y * z)
}
```

该程序运行后输出如下：

```
x =  (1+2i)
y =  (3+4i)
z =  (5+6i)
real(x) =  1
imag(x) =  2
y * z =  (-9+38i)
```

当然，我们可以对声明进行简化，使用自然的方式书写复数：

```go
x := 1 + 2i
y := 3 + 4i
z := 5 + 6i
```

如果一个浮点数面值或一个十进制整数面值后面跟着一个 `i` ( `1i` 的 `1` 不能省略)，它将构成一个复数的虚部，复数的实部是 `0` ：

```go
fmt.Println(5i)     // (0+5i)
```

`math/cmplx` 包提供了复数处理的许多函数，例如：

```go
x := -1 + 0i
fmt.Println(cmplx.Abs(x))       // 1
fmt.Println(cmplx.Asin(x))      // (-1.5707963267948966+0i)
fmt.Println(cmplx.Sqrt(x))      // (0+1i)
fmt.Println(cmplx.Phase(x))     // 3.141592653589793
fmt.Println(cmplx.Polar(x))     // 1 3.141592653589793
```
