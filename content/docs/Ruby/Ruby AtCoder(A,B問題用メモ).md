+++
title = "Ruby AtCoder(A,B問題用メモ)"
author = ["wtnbjn"]
tags = ["Ruby", "Reference"]
draft = false
+++

普段Rubyを全然書かないので、少しAtCoderから離れると構文とか入出力とか全部忘れてしまう。
忘れたときに見返す為のメモとしてここに記録しておく。


## 文字列内の変数展開 {#文字列内の変数展開}

ダブルクォート内で `#{}` 。シングルクォートだと展開できない。

```ruby
name = "Ruby"
puts "Hello, #{name}!"  # => "Hello, Ruby!"
```


## 文字列はchompする {#文字列はchompする}

しないと改行文字が含まれる。

```ruby
s = gets.chomp
```


## 一時変数の省略にはthenを使う {#一時変数の省略にはthenを使う}

```ruby
puts gets.chomp.then{ |s| s == 'no_no' || s > '999' ? 'No' : 'Yes' }
```


## 0パディングはrjust {#0パディングはrjust}

```ruby
num = 42
puts num.to_s.rjust(5, '0')  # => "00042"
```


## substringは[x..y] {#substringは-x-dot-dot-y}

```text
i = gets.chomp[3..].to_i
```


## 連続した範囲(Range) {#連続した範囲--range}

`(x..y)` もしくは `(x...y)` 。ドット3つは終端を含まない(半開範囲)

```ruby
puts (1..349).reject{ |x| x == 316 }
```
