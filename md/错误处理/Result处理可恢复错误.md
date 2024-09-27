<!--
 * @Author: matiastang
 * @Date: 2024-09-27 11:13:58
 * @LastEditors: matiastang
 * @LastEditTime: 2024-09-27 11:30:09
 * @FilePath: /rust-learn/md/错误处理/Result处理可恢复错误.md
 * @Description: Result处理可恢复错误
-->
# Result处理可恢复错误

## 传播错误

当编写一个其实先会调用一些可能会失败的操作的函数时，除了在这个函数中处理错误外，还可以选择让调用者知道这个错误并决定该如何处理。这被称为 传播（propagating）错误，这样能更好的控制代码调用，因为比起你代码所拥有的上下文，调用者可能拥有更多信息或逻辑来决定应该如何处理错误。

例如，示例 9-6 展示了一个从文件中读取用户名的函数。如果文件不存在或不能读取，这个函数会将这些错误返回给调用它的代码：

文件名：src/main.rs

```rs
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let username_file_result = File::open("hello.txt");

    let mut username_file = match username_file_result {
        Ok(file) => file,
        Err(e) => return Err(e),
    };

    let mut username = String::new();

    match username_file.read_to_string(&mut username) {
        Ok(_) => Ok(username),
        Err(e) => Err(e),
    }
}
```

## 传播错误的简写：? 运算符
示例 9-7 展示了一个 read_username_from_file 的实现，它实现了与示例 9-6 中的代码相同的功能，不过这个实现使用了 ? 运算符：

文件名：src/main.rs
```rs
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username_file = File::open("hello.txt")?;
    let mut username = String::new();
    username_file.read_to_string(&mut username)?;
    Ok(username)
}
```
示例 9-7：一个使用 ? 运算符向调用者返回错误的函数

Result 值之后的 ? 被定义为与示例 9-6 中定义的处理 Result 值的 match 表达式有着完全相同的工作方式。如果 Result 的值是 Ok，这个表达式将会返回 Ok 中的值而程序将继续执行。如果值是 Err，Err 将作为整个函数的返回值，就好像使用了 return 关键字一样，这样错误值就被传播给了调用者。

**提示** match 表达式与 ? 运算符所做的有一点不同：? 运算符所使用的错误值被传递给了 from 函数，它定义于标准库的 From trait 中，其用来将错误从一种类型转换为另一种类型。当 ? 运算符调用 from 函数时，收到的错误类型被转换为由当前函数返回类型所指定的错误类型。这在当函数返回单个错误类型来代表所有可能失败的方式时很有用，即使其可能会因很多种原因失败。

`?` 运算符可以实现链式调用。

## 哪里可以使用 ? 运算符
? 运算符只能被用于返回值与 ? 作用的值相兼容的函数。因为 ? 运算符被定义为从函数中提早返回一个值，这与示例 9-6 中的 match 表达式有着完全相同的工作方式。示例 9-6 中 match 作用于一个 Result 值，提早返回的分支返回了一个 Err(e) 值。函数的返回值必须是 Result 才能与这个 return 相兼容。
