+++
title = "Expression(式) and Statement(文)"
author = ["wtnbjn"]
tags = ["Rust", "Reference"]
draft = false
+++

## Expression(式) {#expression--式}

値を生成する構文要素。 `1 + 2` , `if true {1} else {2}` など。
(Rustのifはif文でなく、if式)


## Statement(文) {#statement--文}

実行のみで値を変えさない構文要素。 `let x = 5;` など。


## セミコロン {#セミコロン}

Expression(式)の最後にセミコロン(;)を付けると、その式はStatement(文)に変わり
値を返さなくなる。

```rust
fn example() {
    let x = 5; // これは文。セミコロンが付いているため、値を返さない
    let y = { 3 + 2 }; // このブロック全体は式。最終行にセミコロンがないため5が返る
    let z = { 4; }; // セミコロンがあるため、zには()（ユニット）が代入される
}
```
