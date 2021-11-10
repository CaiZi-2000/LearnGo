# 6. 布尔型

关于 <mark style="color:blue;">**布尔(bool)**</mark> 类型，无非就是两个值： <mark style="color:blue;">**true**</mark> 或者 <mark style="color:blue;">**false**</mark> 。

如果你学过 Python 就会知道真值用 `True` 表示，并且与 `1` 是相等的；而假值用 `False` 表示，并且与 `0` 相等。但是在 Go 中，真值是用 `true` 表示，并且 <mark style="color:blue;">**不与**</mark> `1` 相等；同样的，假值是用 `false` 表示，并且 <mark style="color:blue;">**不与**</mark> `0` 相等。从而在 Go 中不能像在 Python 中一样用布尔值和 `0` 或 `1` 进行比较。

所以，如果你像在 Go 中实现和 Python 类似的布尔值与 `0` 或 `1` 进行比较的功能，需要自己去实现相应的函数。下面提供了相应的两个函数供你参考。

```go
// bool to int
func btoi(b bool) int {
    if b {
        return 1
    }
    return 0
}
```

```go
// int to bool
func itob(i int) bool { 
    return i != 0 
}
```

`if` 和 `for` 语句的条件部分都是布尔类型的值，并且 `==` 和 `<` 以及 `>` 等比较操作也会产生布尔型的值。一元操作符 `!` 对应逻辑非操作，二元操作符 `&&` 和 `||` 分别对应逻辑与和逻辑或操作。其中 `&&` 的优先级比 `||` 高。下面是一个例子：

```go
package main

import (
	"fmt"
)

func main() {
	a := true
	b := false
	fmt.Println("a = ", a)
	fmt.Println("b = ", b)
	fmt.Println("true && false = ", a && b)
	fmt.Println("true || false = ", a || b)
}
```

该程序输出如下：

```
a =  true
b =  false
true && false =  false
true || false =  true
```

其中 `a` 赋值为 `true` ， `b` 赋值为 `false` 。 `a && b` 仅当 `a` 和 `b` 都为 `true` 时，操作符 `&&` 才返回 `true` 。 `a || b` 仅当 `a` 或者 `b` 为 `true` 时，操作符 `||` 返回 `true` 。
