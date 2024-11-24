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


## 配列をQueue/Stackとして扱う {#配列をqueue-stackとして扱う}

-   `push`: 末尾に追加
-   `shift`: 先頭から削除
-   `pop`: 末尾から削除

<!--listend-->

```ruby
queue = [1, 2, 3, 4, 5]
puts queue.shift  # => 1
queue.push(6)
puts queue.inspect  # => [2, 3, 4, 6]
```

```ruby
stack = [1, 2, 3, 4]
element = stack.pop
puts element  # => 4
puts stack.inspect  # => [1, 2, 3]
```


## nilエラーを回避しながらメソッドを呼び出す {#nilエラーを回避しながらメソッドを呼び出す}

`&.` (セーブナビゲーション演算子) を使う

```ruby
m = h.find_index{ |x| x > a }
puts m&.+(2) || -1
```


## スプラット演算子 {#スプラット演算子}

```ruby
a, *h = gets.split.map(&:to_i)
```

-   a, \*h = ... の形式で、多重代入を利用して最初の要素を a に、残りを配列 h に代入します。
-   \*h の \* はスプラット演算子で、残りの全ての要素を配列として受け取ります。
