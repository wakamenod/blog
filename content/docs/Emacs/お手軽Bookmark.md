+++
title = "お手軽Bookmark"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = false
+++

とりあえず `consult-bookmark` を既存のbookmark-jumpコマンド(`C-x r b`)と置き換えておけばOK。
`consult-bookmark` からブックマークの一覧表示も登録もどちらも出来る。

また、 `consult-buffer` で `m SPC` を入力してもブックマーク一覧になる。

登録したブックマークを編集したいときは、 `M-x edit-bookmarks` で **Bookmark List** バッファが表示される。
バッファ内で `?` を入力すると操作コマンドが確認できる。以下、よく使いそうなやつ。

| コマンド | 説明                      |
|------|-------------------------|
| RET  | ブックマークに移動。      |
| o    | リストを残しつつ別ウィンドウでブックマークに移動。 |
| r    | ブックマークの名前を変更  |
| d    | 削除マークを付ける。      |
| x    | 削除マークされたブックマークを削除。 |


## 参考 {#参考}

[Emacs: Bookmarks](https://arialdomartini.github.io/emacs-bookmarks)
