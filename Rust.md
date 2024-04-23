# 数据类型



## Scalar标量

**标量**（*scalar*）类型代表一个单独的值。Rust 有四种基本的标量类型：整型、浮点型、布尔类型和字符类型。



### 整型

>  Rust 中的整型

| 长度    | 有符号  | 无符号  |
| ------- | ------- | ------- |
| 8-bit   | `i8`    | `u8`    |
| 16-bit  | `i16`   | `u16`   |
| 32-bit  | `i32`   | `u32`   |
| 64-bit  | `i64`   | `u64`   |
| 128-bit | `i128`  | `u128`  |
| arch    | `isize` | `usize` |

==整形型默认i32==

`isize` 和 `usize` 类型依赖运行程序的计算机架构：64 位架构上它们是 64 位的，32 位架构上它们是 32 位的。

可以使用表格 3-2 中的任何一种形式编写数字字面值。请注意可以是多种数字类型的数字字面值允许使用类型后缀，例如 `57u8` 来指定类型，同时也允许使用 `_` 做为分隔符以方便读数，例如`1_000`，它的值与你指定的 `1000` 相同。



> Rust 中的整型字面值

|          数字字面值           | 例子          |
| :---------------------------: | ------------- |
|       Decimal (十进制)        | `98_222`      |
|     Hex (十六进制)  (0x)      | `0xff`        |
|     Octal (八进制)  (0o)      | `0o77`        |
|     Binary (二进制)  (0b)     | `0b1111_0000` |
| Byte (单字节字符)(仅限于`u8`) | `b'A'`        |

那么该使用哪种类型的数字呢？如果拿不定主意，Rust 的默认类型通常是个不错的起点，数字类型默认是 `i32`。`isize` 或 `usize` 主要作为某些集合的索引。

[integer overflow(整型溢出)](https://kaisery.github.io/trpl-zh-cn/ch03-02-data-types.html#%E6%95%B4%E5%9E%8B%E6%BA%A2%E5%87%BA)



### 浮点型

Rust 也有两个原生的 **浮点数**（*floating-point numbers*）类型，它们是带小数点的数字。Rust 的浮点数类型是 `f32` 和 `f64`，分别占 32 位和 64 位。默认类型是 `f64`，因为在现代 CPU 中，它与 `f32` 速度几乎一样，不过精度更高。所有的浮点型都是有符号的。

~~~rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
~~~



### 布尔型

正如其他大部分编程语言一样，Rust 中的布尔类型有两个可能的值：`true` 和 `false`。Rust 中的布尔类型使用 `bool` 表示。例如：

~~~rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
~~~



### 字符类型

Rust 的 `char` 类型是语言中最原生的字母类型。下面是一些声明 `char` 值的例子：

~~~rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
~~~

注意，我们用单引号声明 `char` 字面量，而与之相反的是，使用双引号声明字符串字面量。Rust 的 `char` 类型的大小为四个字节 (four bytes)，并代表了一个 Unicode 标量值（Unicode Scalar Value），这意味着它可以比 ASCII 表示更多内容。在 Rust 中，带变音符号的字母（Accented letters），中文、日文、韩文等字符，emoji（绘文字）以及零长度的空白字符都是有效的 `char` 值。Unicode 标量值包含从 `U+0000` 到 `U+D7FF` 和 `U+E000` 到 `U+10FFFF` 在内的值。不过，“字符” 并不是一个 Unicode 中的概念，所以人直觉上的 “字符” 可能与 Rust 中的 `char` 并不符合。第八章的 [“使用字符串储存 UTF-8 编码的文本”](https://kaisery.github.io/trpl-zh-cn/ch08-02-strings.html#使用字符串储存-utf-8-编码的文本) 中将详细讨论这个主题。









## Compound type复合类型

**复合类型**（*Compound types*）可以将多个值组合成一个类型。Rust 有两个原生的复合类型：元组（tuple）和数组（array）。



### tuple





### array







# 所有权





# 引用 



引用可以做到使用该变量但不获得该变量的所有权.

> 不使用引用

~~~rust
fu main(){
    let a=String::from("Hello");
    take_ownership(a);
    println!("{}",a);	//编译不通过,a的所有权已被move给take_ownership函数,函数结束后被销毁.
}

fn take_ownership(some_string: String) {
    println!("{}", some_string);
}
~~~

> 使用引用

~~~rust
fu main(){
    let a=String::from("Hello");
    just_borrow(&a);
    println!("{}",a);	//编译通过,函数只是借用a的值,不改变所有权
}

fn just_borrow(some_string: &String) {
    println!("{}", some_string);
}
~~~



## 可变引用



引用默认不能修改原变量的值



# 切片

