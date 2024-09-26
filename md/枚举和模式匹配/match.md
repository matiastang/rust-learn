<!--
 * @Author: matiastang
 * @Date: 2024-09-26 16:26:15
 * @LastEditors: matiastang
 * @LastEditTime: 2024-09-26 16:34:30
 * @FilePath: /rust-learn/md/枚举和模式匹配/match.md
 * @Description: match
-->
# match

Rust 有一个叫做 match 的极为强大的控制流运算符，它允许我们将一个值与一系列的模式相比较，并根据相匹配的模式执行相应代码。模式可由字面值、变量、通配符和许多其他内容构成；第十八章会涉及到所有不同种类的模式以及它们的作用。match 的力量来源于模式的表现力以及编译器检查，它确保了所有可能的情况都得到处理。
match 还有另一方面需要讨论：这些分支必须覆盖了所有的可能性。

当 match 表达式执行时，它将结果值按顺序与每一个分支的模式相比较。如果模式匹配了这个值，这个模式相关联的代码将被执行。如果模式并不匹配这个值，将继续执行下一个分支，非常类似一个硬币分类器。

**想法**有点儿像`Swift`中的`Switch`，也是有编译器检查，确保没有遗漏。和一些语言的`Switch`有点儿不一样，大部分语言的`Switch`是没有编译器检查是否有遗漏的。

Rust 还提供了一个模式，当我们不想使用通配模式获取的值时，请使用 _ ，这是一个特殊的模式，可以匹配任意值而不绑定到该值。这告诉 Rust 我们不会使用这个值，所以 Rust 也不会警告我们存在未使用的变量。
```rs
let config_max = Some(3u8);
if let Some(max) = config_max {
    println!("The maximum is configured to be {max}");
}
```
```rs
let mut count = 0;
match coin {
    Coin::Quarter(state) => println!("State quarter from {state:?}!"),
    _ => count += 1,
}
// 或者可以使用这样的 if let 和 else 表达式：


let mut count = 0;
if let Coin::Quarter(state) = coin {
    println!("State quarter from {state:?}!");
} else {
    count += 1;
}
```