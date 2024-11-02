+++
title = "org-download"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = false
+++

org-downloadの使い方について調べたのでメモ。
downloadという名前が若干ややこしく感じるが、ローカル画像をインサートする際の便利機能としても使える。

-   動作環境

> GNU Emacs 30.0.91 (build 1, aarch64-apple-darwin23.6.0, NS appkit-2487.70 Version 14.6.1 (Build 23G93)) of 2024-10-16


## ドラッグ&amp;ドロップ {#ドラッグ-and-ドロップ}

まずドラッグ&amp;ドロップだが、私の環境では正常に動作しない。
Emacs29で本体に導入されたドラッグ&amp;ドロップ機能と競合してるのが原因のようだ。

-   [Integration with emacs 29 and native drag and drop support #215](https://github.com/abo-abo/org-download/issues/215)

`org-download-image-dir` はorg-downloadでダウンロードした画像の保存先として指定されているが、
ドラッグ&amp;ドロップ時にはこの設定が使われず、カレントフォルダ内のdataフォルダに画像が保存されてしまう。
あと、これは私の環境の問題かもしれないが、挿入されるインライン画像のパスがずれてしまう。


## コマンド {#コマンド}

以下のコマンドを使用することで、画像ファイルを保存し、インライン画像として挿入できる。
画像の保存先は `org-download-image-dir` で指定したフォルダになる。


### org-download-image {#org-download-image}

このコマンドを実行すると、ミニバッファに入力したURLの画像がダウンロードされ、挿入される。


### org-download-clipboard {#org-download-clipboard}

クリップボードにコピーした画像を挿入する。
このコマンドを使う場合、MacOSでは `pngpaste` のインストールが必要となる。

```bash
brew install pngpaste
```


### org-download-yank {#org-download-yank}

kill-ringに保存されたURLまたはファイルパスの画像をダウンロードして挿入する。
Diredでファイルパスを取得するには、 `0 w` コマンドを使用する。


### org-download-screenshot {#org-download-screenshot}

このコマンドを実行すると、スクリーンショットを取得するためのアプリケーションが起動し、
OSのカーソルがスクリーンショットの範囲選択に切り替わる。
取得したスクリーンショットは、指定した場所に挿入される。
デフォルトではスクリーンショットのアプリケーションが `gnome-screenshot` になっており
MacOS用に設定を変更する必要があった。

```emacs-lisp
(setq org-download-screenshot-method "screencapture -i %s")
```
