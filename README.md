<!-- vscode-markdown-toc -->
* 1. [`Rust`](#Rust)
	* 1.1. [安装更新](#)
* 2. [`Cargo`](#Cargo)
	* 2.1. [安装更新](#-1)
	* 2.2. [使用](#-1)
	* 2.3. [发布（release）构建](#release)
* 3. [参考](#-1)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

<!--
 * @Author: matiastang
 * @Date: 2021-09-14 09:22:59
 * @LastEditors: matiastang
 * @LastEditTime: 2024-09-25 10:41:02
 * @FilePath: /rust-learn/README.md
 * @Description: README
-->

# rust-learn

`Rust`学习相关内容

##  1. <a name='Rust'></a>`Rust`

###  1.1. <a name=''></a>安装更新

1. `Rust`安装

[`Rust`安装](https://kaisery.github.io/trpl-zh-cn/ch01-01-installation.html)

2. 查看`Rust`版本
```sh
$ rustc --version
rustc 1.81.0 (eeb90cda1 2024-09-04)
```

3. 更新`Rust`
```sh
$ rustup update
info: syncing channel updates for 'stable-aarch64-apple-darwin'
info: checking for self-update

  stable-aarch64-apple-darwin unchanged - rustc 1.81.0 (eeb90cda1 2024-09-04)

info: cleaning up downloads & tmp directories
```

##  2. <a name='Cargo'></a>`Cargo`

###  2.1. <a name='-1'></a>安装更新

1. `Cargo`安装

官方安装包的话，则自带了 `Cargo`。[`Rust`安装](https://kaisery.github.io/trpl-zh-cn/ch01-01-installation.html)

2. `Cargo`版本
```sh
$ cargo --version
cargo 1.81.0 (2dbb1af80 2024-08-20)
```

###  2.2. <a name='-1'></a>使用

* 创建项目
```sh
$ cargo new project_name
```

* 进入项目目录
```sh
$ cd project_name
```
创建项目后会生成`Cargo.lock`和`Cargo.toml`文件。

* 编译项目
```sh
$ cargo build
```
编译后会生成`target`目录。可执行文件 `target/debug/hello_cargo` （在 `Windows` 上是 `target\debug\hello_cargo.exe`），而不是放在目前目录下。由于默认的构建方法是调试构建（`debug build`），`Cargo` 会将可执行文件放在名为 `debug` 的目录中。可以通过这个命令运行可执行文件：
```sh
$ ./target/debug/hello_cargo # 或者在 Windows 下为 .\target\debug\hello_cargo.exe
Hello, world!
```

* 使用 `cargo run` 在一个命令中同时编译并运行生成的可执行文件
```sh
$ cargo run
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/hello_world`
Hello, world!
```

* `Cargo` 还提供了一个叫 `cargo check` 的命令。该命令快速检查代码确保其可以编译，但并不产生可执行文件
```sh
$ cargo check
    Checking hello_world v0.1.0 (/Users/matias/matias/MT/MTGithub/Rust/rust-learn/hello_world)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.09s
```

使用 `Cargo` 的一个额外的优点是，不管你使用什么操作系统，其命令都是一样的

###  2.3. <a name='release'></a>发布（release）构建

当项目最终准备好发布时，可以使用 `cargo build --release` 来优化编译项目。这会在 `target/release` 而不是 `target/debug` 下生成可执行文件。这些优化可以让 `Rust` 代码运行的更快，不过启用这些优化也需要消耗更长的编译时间。这也就是为什么会有两种不同的配置：
一种是为了开发，你需要经常快速重新构建；
另一种是为用户构建最终程序，它们不会经常重新构建，并且希望程序运行得越快越好。如果你在测试代码的运行时间，请确保运行 `cargo build --release` 并使用 `target/release` 下的可执行文件进行测试。

##  3. <a name='-1'></a>参考

[Rust Github](https://github.com/rust-lang/rust)
[Rust Learn](https://www.rust-lang.org/learn#learn-use)
[Rust 程序设计语言 简体中文版](https://kaisery.github.io/trpl-zh-cn/title-page.html)
