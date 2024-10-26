+++
title = "Go開発向けパッケージ"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = true
+++

Go向けの知らないパッケージをいくつか見つけたので、忘れないようにまとめておく。


## [go-tag](https://github.com/brantou/emacs-go-tag) {#go-tag}

-   `M-x go-tag-add`
-   `M-x go-tag-remove`
-   `M-x go-tag-refresh`

タグの記法（キャメルケースなど）の設定は以下で変更できる。

```emacs-lisp
(setq go-tag-args (list "-transform" "camelcase"))
```


## [go-playground](https://github.com/grafov/go-playground) {#go-playground}

-   `M-x go-playground`

Playground用のバッファが開くので、試したいコードをそのまま書き込む。
`C-<return>` でファイルを保存し、コードを実行できる。
play.golang.org へのアップロード用コマンドもある。


## [go-gen-test](https://github.com/s-kostyaev/go-gen-test) {#go-gen-test}

-   `M-x go-gen-test-dwim`

テストコードを自動生成する。プロジェクトによってテストの書き方が異なることが多いので、使用頻度は低いかもしれない。


## [go-impl](https://github.com/emacsorphanage/go-impl) {#go-impl}

-   `M-x go-impl`

    Interfaceを満たす構造体を定義する機能がある。


## [go-stacktracer](https://github.com/samertm/go-stacktracer.el) {#go-stacktracer}

-   `M-x go-stacktracer-region`

Panicが発生した際、Stacktraceのログを選択して `M-x go-stacktracer-region` を実行すると、新しいバッファが開き、
そこからファイルにジャンプできるようになる。


## Other {#other}

[yasnippet-capf](https://github.com/elken/yasnippet-capf) があったので追加した。[go-snippets](https://github.com/toumorokoshi/go-snippets) のスニペットがcapeで補完されることを確認済み。
