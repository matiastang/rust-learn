<!--
 * @Author: matiastang
 * @Date: 2024-09-27 11:14:40
 * @LastEditors: matiastang
 * @LastEditTime: 2024-09-27 11:14:48
 * @FilePath: /rust-learn/md/错误处理/README.md
 * @Description: README
-->
# Rust 错误处理

Rust 将错误分为两大类：可恢复的（recoverable）和 不可恢复的（unrecoverable）错误。对于一个可恢复的错误，比如文件未找到的错误，我们很可能只想向用户报告问题并重试操作。不可恢复的错误总是 bug 出现的征兆，比如试图访问一个超过数组末端的位置，因此我们要立即停止程序。

大多数语言并不区分这两种错误，并采用类似异常这样方式统一处理它们。Rust 没有异常。相反，它有 Result<T, E> 类型，用于处理可恢复的错误，还有 panic! 宏，在程序遇到不可恢复的错误时停止执行