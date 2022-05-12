# go

# 编程之前

## 注释

> 尽量用行注释

```go
//  行注释
/*
段落注释
*/
```

## 格式化代码工具

> go自带了将代码格式化的工具gmfmt

```shell
gofmt -w xxx.go
```

## 代码风格

```go
// 括号风格
func main()  // 编译不过去
{
  pass
}


func main(){  // 可以编译
  pass
}

// 空格风格
var num = a + b
// 换行风格，每行不超过80个字符,逗号换行
fmt.println("aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
            "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
            "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa")
```

# 变量

## 声明变量

注意:

> 该区域的变量值可以在同一类型范围内不断变化
>
> 变量在同一个作用域内不能重名
>
> 变量 = 变量名 + 值 + 数据类型
>
> 变量如没有被赋值，会被使用默认值int=0,string=""

| 数据类型 | 默认值 |
| -------- | ------ |
| 整型     | 0      |
| 浮点型   | 0      |
| 字符串   | ""     |
| 布尔类型 | false  |



```go
/*
- 指定类型，不赋值，使用默认值（int 默认0）
- 根据值自动判定类型
- 省略var，注意:=左侧的变量不应该是已经声明过的，否则会导致编译错误
- 多变量声明
*/
package main
import "fmt"

func main(){
	// 定义变量
	var i int // 默认为0
  // 赋值
	i = 10
	fmt.Println("i=", i)
  
  // 自动判定类型
  var num = 10.10
  fmt.Println("num=", num)
  // 省略 var 并赋值 用:= 
  name := "Tom"
  fmt.Println("name=", name)
  
  // 一次性声明多个变量
  var n1, n2, n3 int
  fmt.Println("多变量var声明", n1, n2, n3)
  var a1, a2, a3  = "1","2","3"
  fmt.Println("多变量声明并赋值", a1, a2, a3)
  b1, b2, b3 :=  "Tom", 23, "man"
  fmt.Println("多变量声明并赋值并自动判断类型", b1, b2, b3)

}

// 定义全局变量
var c1 = "henry"
var c2 = "tom"
var c3 = "jack"
// 多变量声明全局变量
var (
  d1 = "henry"
  d2 = "tom"
  d3 = "jack"
)
```

# 数据类型

## 基本数据类型

数值：

> 整型：uint,uint8,uint16,uint32,uint64
>
> 浮点型：float32,float64

字符型：byte 

布尔型：FALSE，TRUE

字符串：string

复数：complex64，complex128

特殊：

>  rune:（不完全等价于int32,表示一个Unicode码点）

## 复杂数据类型

- 指针
- 数组
- 结构体：不完全等价于class类
- 管道
- 函数
- 切片：动态数组
- 接口
- map：不完全等价于集合

### 整型 

| 类型  | 有无符号 | 占用空间 | 数据范围       |
| ----- | -------- | -------- | -------------- |
| int8  | 有       | 1字节    | -128 ~ 127     |
| int16 | 有       | 2字节    | -2^15 ~ 2^15-1 |
| int32 | 有       | 4字节    | -2~31 ~ 2~31-1 |
| int64 | 有       | 8字节    | -2^63 ~ 263-1  |

| 类型   | 有无符号 | 占用空间 | 数据范围   |
| ------ | -------- | -------- | ---------- |
| uint8  | 无       | 1字节    | 0 ~ 255    |
| uint16 | 无       | 2字节    | 0 ~ 2^6-1  |
| uint32 | 无       | 4字节    | 0 ~ 2^23-1 |
| uint64 | 无       | 8字节    | 0 ~ 2^64-1 |

| 类型 | 有无符号 | 占用空间                             | 数据范围                           | 备注                         |
| ---- | -------- | ------------------------------------ | ---------------------------------- | ---------------------------- |
| int  | 有       | 32位系统4个字节<br />64位系统8个字节 | -2^31 ~ 2^31-1<br />-2^63 ~ 2^63-1 |                              |
| uint | 无       | 32位系统4个字节<br />64位系统8个字节 | 0 ~ 2^32-1<br />0 ~ 2^31-1         |                              |
| rune | 有       | 与int32一样                          | 0 ~ 2^23-1                         | 等价int32，表示一个Unicode码 |
| byte | 无       | 与uint8等价                          | 0 ~ 255                            | 当腰存储字符时选用byte       |

```go
package main

import (
	"fmt"
	"unsafe"
)

func main() {
	var i int
	i = 10
	fmt.Printf("变量i，类型是 %T，占用的空间是：%d", i, unsafe.Sizeof(i))
}
```

### 浮点数

- 浮点数 = 浮点位 + 指数位 + 尾数位
- 尾数位可能丢失，造成精度损失
- float64精度比flaot32准确

| 类型    | 占用空间 | 数据范围                 |
| ------- | -------- | ------------------------ |
| float32 | 4字节    | -3.403E38 ~ 3.403E38     |
| float64 | 8字节    | -1.798E308 到 +1.798E308 |

注意：

> - 浮点型不受操作系统位数影响
> - 默认float64声明
> - 浮点数有两种表现形式：
>   - 十进制：0.53 等价 .53
>   - 科学计数法：5.1234E2（相当于：5.123 * 10^2） 5.123E-2(相当于5.123 / 10^2)

### 字符型

> go中没有特定的字符型类型，存储单个字符一般用byte

```go
package main

import (
	"fmt"
	"unsafe"
)

func main() {
	var i byte
	i = 'a'
	fmt.Printf("i变量值为：%c，类型是%T，占位是%d", i, i, unsafe.Sizeof(i))
}

```

注意：

- 字符使用单引号括起来
- 存储的是int8类型数字，想要输出ascii码格式化输出用%c

### 布尔类型

```go
package main

import (
	"fmt"
)

func main() {
	var f = false

	fmt.Printf("t变量值为:", f)

}

```

### 字符串类型

- 字符串一旦赋值，就不能修改，字符串是不可变的
- 字符串用双引号声明
- 多段字符串用反引号 
- 字符串拼接 +（多行拼接，要把+号留在上一行） 和 += 

```go
package main

import (
	"fmt"
)

func main() {
	var s string
	s = `这
		是
		一个
		字符
		传`
	var str string
	str = "\n这是一个字符串"

	var str2 string
	str2 = "这是一个" +
		"字符串"

	fmt.Printf("s变量值为:%s", s)
	fmt.Printf("s变量值为:%s", str)
	fmt.Printf("s变量值为:%s", str2)
}
```

## 数据转换

### 整数类型转换

- 数据类型可以范围大或范围小相互之间转换int8 <=>i nt64
- 被转换的数据变量并不受影响（变量指引不会被替换）
- 范围大的数据类型转换到小的数据类型，数据做溢出处理可编译不报错，但数据值不对
- 同一种类型不同范围的不能直接运算：int8 不能直接 + int64

```go
package main

import "fmt"

func main() {
	var num_8 int8
	var num_64 int64
	num_64 = 99999999
	num_8 = int8(num_64)
	fmt.Printf("数据类型转换，int8的数值是%d，数据溢出了\n", num_8)  // 数据类型转换，int8的数值是-1，数据溢出了
	num_8 = 120
	num_64 = int64(num_8)
	fmt.Printf("数据类型转换，int8的数值是%d，数据溢出了\n", num_64) // 数据类型转换，int8的数值是120，数据溢出了

}

```

### 字符串类型转换

通用：

```
%v	值的默认格式表示
%+v	类似%v，但输出结构体时会添加字段名
%#v	值的Go语法表示
%T	值的类型的Go语法表示
%%	百分号
```

布尔值：

```
%t	单词true或false
```

整数：

```
%b	表示为二进制
%c	该值对应的unicode码值
%d	表示为十进制
%o	表示为八进制
%q	该值对应的单引号括起来的go语法字符字面值，必要时会采用安全的转义表示
%x	表示为十六进制，使用a-f
%X	表示为十六进制，使用A-F
%U	表示为Unicode格式：U+1234，等价于"U+%04X"
```

浮点数与复数的两个组分：

```
%b	无小数部分、二进制指数的科学计数法，如-123456p-78；参见strconv.FormatFloat
%e	科学计数法，如-1234.456e+78
%E	科学计数法，如-1234.456E+78
%f	有小数部分但无指数部分，如123.456
%F	等价于%f
%g	根据实际情况采用%e或%f格式（以获得更简洁、准确的输出）
%G	根据实际情况采用%E或%F格式（以获得更简洁、准确的输出）
```

字符串和[]byte：

```
%s	直接输出字符串或者[]byte
%q	该值对应的双引号括起来的go语法字符串字面值，必要时会采用安全的转义表示
%x	每个字节用两字符十六进制数表示（使用a-f）
%X	每个字节用两字符十六进制数表示（使用A-F）    
```

指针：

```
%p	表示为十六进制，并加上前导的0x
```

### 转成字符串

#### fmt.Sprintf

```go
package main

import "fmt"

func main() {
	var num1 int = 99
	var num2 float64 = 3.456
	var b bool = true
	var mychar byte = 'h'
	var str string

	str = fmt.Sprintf("%d", num1)
	fmt.Printf( "str type %T str=%q\n", str, str)

	str = fmt.Sprintf("%f ", num2)
	fmt.Printf( "str type %T str=%q\n", str, str)

	str = fmt.Sprintf("%t", b)
	fmt.Printf( "str type %T str=%q\n", str, str)

	str = fmt.Sprintf("%c", mychar)
	fmt.Printf( "str type %T str=%q\n", str, str)
}

/*
str type string str="99"
str type string str="3.456000 "
str type string str="true"
str type string str="h"

*/
```

#### strconv

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	var num1 int = 99
	var num2 float64 = 3.456
	var b bool = true
	var str string

	str = strconv.FormatInt(int64(num1), 10)
	fmt.Printf( "str type %T str=%q\n", str, str)

	// 变量 类型 保留小数位 变量范围
	str = strconv.FormatFloat(num2, 'f', 10, 64)
	fmt.Printf( "str type %T str=%q\n", str, str)

	str = strconv.FormatBool(b)
	fmt.Printf( "str type %T str=%q\n", str, str)

	var num3 int64 = 1234
	str = strconv.Itoa(int(num3))
	fmt.Printf( "str type %T str=%q\n", str, str)

}

/*
str type string str="99"
str type string str="3.4560000000"
str type string str="true"
str type string str="1234"

*/
```

### 字符串转基础类型

 









