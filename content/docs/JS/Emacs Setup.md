+++
title = "Emacs Setup"
author = ["wtnbjn"]
tags = ["JS", "Reference"]
draft = false
+++

新しいinit.elに切り替えてから、しばらくtypescriptを触る機会が無かったが
久し振りにソースを開いたらLSPが動かなくて困った。以前は `web-mode` をlsp-modeで起動してたはずなのだけど
新しい環境だと動かなくなってた。Emacsのバージョンが上ったせい?

とりあえず、Eglotで `typescript-language-server` を起動するように設定し難を逃れる。


## 参考 {#参考}

-   [Setting Up TypeScript and Eslint With Eglot](https://notes.alexkehayias.com/setting-up-typescript-and-eslint-with-eglot/)
-   [Modern Emacs Typescript Web (React) Config with lsp-mode, treesitter, tailwind, TSX &amp; more](https://www.ovistoica.com/blog/2024-7-05-modern-emacs-typescript-web-tsx-config)
