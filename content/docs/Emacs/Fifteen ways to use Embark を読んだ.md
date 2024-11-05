+++
title = "Fifteen ways to use Embark を読んだ"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = false
+++

<https://karthinks.com/software/fifteen-ways-to-use-embark/>

備忘のためのメモ。


## 1. Open any buffer by splitting any window {#1-dot-open-any-buffer-by-splitting-any-window}

いきなりだが個人的に使わなそうなので詳細は割愛。
内容としては、ファイルを開く際にどのウィンドウを使うか、またはどのウィンドウをスプリットして開くかを
any windowを使って指定するというもの。先にウィンドウを作ってそこで開く方が早くないか?と思ってしまった。
ただ、実際に運用してみて印象が変わるかもしれないので、また機会があったら試してみたい。


## 2. Copy a file to a remote location when finding a file {#2-dot-copy-a-file-to-a-remote-location-when-finding-a-file}

1.  `Find file` などでファイルを絞り込む
2.  `embark-act` -&gt; `c` でコピー先を指定してコピー

`embark-act` の際にプリフィックス(`C-u`) を付けると、find-fileから抜けずに続行できる


## 3. Insert a minibuffer candidate into the buffer {#3-dot-insert-a-minibuffer-candidate-into-the-buffer}

1.  `Find file` などでファイルを絞り込む
2.  `embark-act` -&gt; `i` で現在のバッファにファイル名を挿入する

`I` だと相対パスか、もしくはバッファのコンテンツを挿入できる場合もあるらしいが、試したところバッファの挿入になることは未だない。


## 4. Run a shell command on a minibuffer candidate file without losing your session {#4-dot-run-a-shell-command-on-a-minibuffer-candidate-file-without-losing-your-session}

1.  `Find file` などでファイルを絞り込む
2.  `embark-act` -&gt; `&` で `async-shell-command` 。選択したファイル名が挿入された状態で実行できる。

動画では `file` コマンドを実行していた。たしかに、ファイルを指定してコマンドを実行したい場面は割とよくあるかも。


## 5. Open a file as root without losing your session {#5-dot-open-a-file-as-root-without-losing-your-session}

自PC内でrootを取ってファイル操作したい場面はあまり無いので割愛。


## 6. Upload a region of text to 0x0 {#6-dot-upload-a-region-of-text-to-0x0}

0x0.st というファイル共有サービスがあって、そこにリージョンの内容をアップロードするという内容。
便利だが、自分の場合他人に何かを共有する場面はほとんどが業務に関することなので、利用することは無さそう。


## 7. Visit a package’s URL from the minibuffer {#7-dot-visit-a-package-s-url-from-the-minibuffer}

1.  `Describe package (C-h P)`
2.  `embark-act` -&gt; `u` で `embark-browse-package-url` 。 パッケージのURLがブラウザが開かれる。


## 8. Set a variable from anywhere it appears in a buffer {#8-dot-set-a-variable-from-anywhere-it-appears-in-a-buffer}

1.  elispのバッファで、変数にカーソルを合わせて `embark-act`
2.  `=` で `set-variable` できる


## 9. Add a keybinding for a command name from anywhere it appears {#9-dot-add-a-keybinding-for-a-command-name-from-anywhere-it-appears}

バッファ内のコマンド名から `global-set-key` できるらしい。あまり使う機会は無さそう。


## 10. Export Emacs package candidates to a package menu {#10-dot-export-emacs-package-candidates-to-a-package-menu}

`embark-export` は日頃から使ってるので割愛。


## 11. Collect imenu candidates in an “imenu-list” {#11-dot-collect-imenu-candidates-in-an-imenu-list}

`imenu` を `embark-export` したいモチベーションが分からなかったが、 `imenu` を普段使ってないから分からないだけかもしれない。
便利そうなので積極的に使っていきたい。 取り急ぎ consult-imenuを `M-g i` にセットした。


## 12. Export file candidates to a dired-buffer {#12-dot-export-file-candidates-to-a-dired-buffer}

1.  `Find file` などでファイルを絞り込む
2.  `embark-export` すると絞り込んだファイル一覧でdiredバッファが作られる。

diredになるの知らなかった。


## 13. Export buffer candidates to ibuffer {#13-dot-export-buffer-candidates-to-ibuffer}

バッファ一覧で `embark-export` すると ibufferになる。


## 14. Export variable candidates to a customize buffer {#14-dot-export-variable-candidates-to-a-customize-buffer}

`describe-variable` の変数一覧で `embark-export` するとcustomize bufferになる。
