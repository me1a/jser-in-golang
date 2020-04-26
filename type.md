# 类型

js 中的类型包括 `undefined`、`null`、`Symbol`、`布尔值（Boolean）`、`BigInt`、`字符串（String）`、`数值（Number）`、`对象（Object)`

在 go 中，类型有很多，

| 类型         | 长度 (B) | 默认值 | 说明                                 |
| ------------ | -------- | ------ | ------------------------------------ |
| bool         | 1        | false  |                                      |
| byte         | 1        | 0      | uint8 别名                           |
| int,uint     | 4,8      | 0      | 默认整数类型，依据目标平台，32 或 64 |
| int8,uint8   | 1        | 0      | -128~127,0~255                       |
| int16,uint16 | 2        | 0      | -32768~32767 ,0~65535                |
| int32,uint32 | 4        | 0      | -21 亿~21 亿,0~42 亿                 |
| int64,uint64 | 8        | 0      |                                      |
| float32      | 4        | 0.0    |                                      |
| float64      | 8        | 0.0    | 浮点数默认类型                       |
| complex64    | 8        |        |                                      |
| complex128   | 16       |        |                                      |
| rune         | 4        | 0      | Unicode Code Point, int32 别名       |
| uintptr      | 4,8      | 0      | 足以存指针的 uint                    |
| string       |          | ""     | 默认为空字符串                       |
| array        |          |        | 数组                                 |
| struct       |          |        | 结构体                               |
| function     |          | nil    | 函数                                 |
| interface    |          | nil    | 接口                                 |
| map          |          | nil    | 字典，引用类型                       |
| slice        |          | nil    | 切片，引用类型                       |
| channel      |          | nil    | 通道，引用类型                       |

其中，`nil`类似 js 中的`null`。`uintptr` 类似 C 语言中的指针。在 64 位系统上，类型`int`的长度是 8，和`int64`一样，但这两个不是同一个类型。
go 中，引用类型有三个`slice`、`map`、`channel`，而和 js 中的作为引用类型的 `array` 不一样，`array`在 go 中是基础类型，包含相同元素的数组，在 go 中是相等的。

通常在类型的声明方式中，会用到 `new` 和 `make`

> **new**-这是个用来分配内存的内建函数， 但与其它语言中的同名函数不同，它不会初始化内存，只会将内存置零。 也就是说，new(T) 会为类型为 T 的新项分配已置零的内存空间， 并返回它的地址，也就是一个类型为 \*T 的值。用 Go 的术语来说，它返回一个指针， 该指针指向新分配的，类型为 T 的零值。

> **make** 只用于创建切片、映射和信道，并返回类型为 T（而非 \*T）的一个已初始化 （而非置零）的值。 出现这种用差异的原因在于，这三种类型本质上为引用数据类型，它们在使用前必须初始化

## 类型转换

js 中对于两个不同的类型， 会发生隐式类型转换

```js
const s = "2";
const n = 2;

s == n; // true
```

在 go 中， 两个类型不同的变量无法进行比较，下面的代码会报错

```go
x:=100

if x { // non-bool x (type int) used as if condition

}
```

go 中可以自定义类型

````go
// 代码1
type flags string
var f flags = "go"
var s string = "go"
fmt.Println(f == s) // invalid operation: f == s (mismatched types flags and string)

// 代码2
type str = string
var ss str = "go"
var sss string = "go"
fmt.Println(ss == sss)
    ```
````

代码 1 中，自定义了一个 flags 类型，底层是`string`类型， 虽然底层和值都是一样的， 也不能进行比较。
代码 2 中，是将 str 作为了 `string` 的一个别名，实际上还是一个类型
