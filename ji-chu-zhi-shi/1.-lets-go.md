---
cover: ../.gitbook/assets/Let's Go.png
coverY: 0
---

# 1. Let's Go

### Go 语言简介

Go 又称 Golang ，是 Google 的 Robert Griesemer，Rob Pike 及 Ken Thompson 开发的一种静态强类型、编译型语言。Go 语言语法与 C 相近，但功能上有：内存安全，GC（垃圾回收），结构形态及 CSP-style 并发计算。

### Go 的安装

Go 支持很多主流平台，例如 Windows 、 Mac 、 Linux 等等。首先需要前往 Go 官网下载相应平台的二进制文件，官网地址为：

<mark style="color:blue;">https://golang.org/</mark>

但因为众所周知的原因访问不了，可以访问下面的地址：

<mark style="color:blue;">https://www.jetbrains.com/go/</mark>

当然也可以到 Go 语言中文网下载，Go 语言中文网下载地址为：

<mark style="color:blue;">https://studygolang.com/dl</mark>

#### Windows

在 Go 官网下载 `MSI` 安装程序。安装安装指引程序安装完成后，会将 Golang 安装到 `C:\Program Files\Go` 目录下，同时 `C:\Program Files\Go\bin` 目录也会被添加到 `PATH` 环境变量中。

我使用的是 Windows 操作系统，所以安装完成后，在 `cmd` 中使用命令 `go version` 验证是否安装成功。如果安装成功，会显示 go 的版本信息，例如：

```shell
C:\Users>go version
go version go1.17.2 windows/amd64
```

#### Mac OS

在 Go 官网下载 `pkg` 安装程序。安装安装指引程序安装完成后，会将 Golang 安装到 `/usr/local/go` 目录下，同时 `/usr/local/go/bin` 文件夹也会被添加到 `PATH` 环境变量中。

#### Linux

在 Go 官网下载 `tar.gz` 文件，并解压到 `/usr/local` 。添加 `/usr/local/go/bin` 到 `PATH` 环境变量中。Go 就已经成功安装在 Linux 上了。

### Go IDE 的安装

个人推荐使用 **GoLand** ，GoLand 是 Jetbrains 家族的 Go 语言 IDE，有 30 天的免费试用期。支持系统环境三大平台 Mac 、 Linux 和 Windows 。 GoLand 下载地址为：

<mark style="color:blue;">https://www.jetbrains.com/go/</mark>

**LiteIDE** 是一款开源、跨平台的轻量级 Go 语言集成开发环境（IDE）。但只支持 Windows 和 Linux 。 LiteIDE 下载地址为：

<mark style="color:blue;">http://sourceforge.net/projects/liteide/files/</mark>

当然你也可以使用 **Visual Studio Code** 并安装相应的 Go 扩展来编写 Go 程序。

### 第一个 Go 程序

接下来，我们就从编写第一个 Go 程序开始，学习 Go 语言。

首先，在任意目录下创建一个目录 **hello** 。接着在此目录下创建一个 **hello.go** 文件，打开文件键入下面的代码，保存并退出。

```go
// hello.go
package main

import "fmt"

func main() {
	fmt.Println("Let's go!")
}
```

### 编译运行 Go 程序

首先打开 cmd 窗口，进入存放 **hello.go** 目录下（可以直接在文件资源管理器的地址栏输入 cmd 进入），然后使用命令 `go build hello.go` 编译 **hello.go** 程序，编译完成后，你能在目录下看到多了一个 **hello.exe** 可执行文件。接着同样在 cmd 窗口使用命令 `hello` 运行 **hello.exe** 程序，你会在 cmd 窗口上看到输出了字符串 `Let's go!` 。

```shell
C:\Users\hello>go build hello.go

C:\Users\hello>hello
Let's go!
```

当然，你也可以使用 `go run hello.go` 命令编译链接程序并运行，同样也会输出上面的字符串。但是，使用 `go run` 命令不会在运行目录下生成任何文件，可执行文件被放在临时文件中被执行，工作目录被设置为当前目录。

```shell
C:\Users\hello>go run hello.go
Let's go!
```

### 简析第一个 Go 程序

```go
// hello.go
package main

import "fmt"

func main() {
	fmt.Println("Let's go!")
}
```

首先，第一行是注释语句，跟 C 语言一样，Go 语言也采用 `//` 和 `/* */` 作为注释标记。

其次，在第二行指定了该文件属于 **main** 包。 Go 代码是使用包来组织的，包类似于其他语言中的库和模块。一个包由一个或多个 `.go` 源文件组成，放在一个文件夹中，该文件夹的名字描述了包的作用。每一个源文件的开始都用 `package` 声明，上面的例子里面是 `package main` ，指明了这个文件属于 **main** 包。后面跟着它导入的其他包的列表，然后是存储在文件中的程序声明。名为 `main` 的包比较特殊，它用来定义一个独立的可执行程序，而不是库。在 `main` 包中，函数 `main` 也是特殊的，不管在什么程序中， `main` 做什么事情，它总是程序开始执行的地方。

第四行引入了 **fmt** 包，因为使用了 `fmt` 包中的函数来格式化输出和扫描输入，所以要在这里导入此包。 `Println` 是 `fmt` 中一个基本的输出函数，它输出一个或多个用空格分隔的值，结尾使用一个换行符，这样看起来这些值是单行输出。 Go 的标准库中有 100 多个包用来完成输入、输出、排序、文本处理等常规任务。在 Go 程序中，我们需要告诉编译器源文件需要哪些包，用 `package` 声明后面的 `import` 来导入这些包。我们必须精确地导入需要的包。在缺失导入或存在不需要的包的情况下，编译都会失败，这种严格的要求可以防止程序演化中引用不需要的包。 `import` 声明必须跟在 `package` 声明之后。

第六行我们定义了一个 **main** 函数，该函数是一个特殊的函数，整个程序从 **main** 函数开始运行。 mian 函数必须放在 main 包中。其中的 `{` 和 `}` 分别表示函数的开始和结束部分。特别注意，在 Go 中不需要在语句或声明后面使用分号结尾，除非有多个语句或声明出现在同一行。事实上，跟在特定符号后面的换行符被转换为分号，在什么地方进行换行会影响对 Go 代码的解析。例如， `{` 符号必须和关键字 `func` 在同一行，不能独自成行，并且在 `x+y` 这个表达式中，换行符可以在 `+` 操作符的后面，但是不能在 `+` 操作符的前面。Go 对于代码的格式化要求非常严格。我们可以使用 `gofmt` 工具将代码以标准格式重写， `go` 工具的 `fmt` 子命令使用 `gofmt` 工具来格式化指定包里的所有文件或者当前文件夹中的文件(默认情况下)。

第七行我们使用 `fmt` 包中的 `Println` 函数把文本写入标准输出。
