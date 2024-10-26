+++
title = "Orgモードで数式をプレビューするためのLaTeX設定"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = false
+++

Emacsで数式をプレビューするためのLaTeX環境を構築した。

"Emacs", "LaTeX"、で検索するとLaTeXで執筆するための解説記事が出てくるが、
私はOrgモードで数式プレビューができれば十分なので、そのための最小限の設定をまとめた。

-   対象環境: MacOS


## インストール {#インストール}

GUIなしのMacTeXをインストールするために、以下のコマンドを実行。

```emacs-lisp
brew install --cask mactex-no-gui
```


## Elisp {#elisp}

AUCTeXをインストールし、以下の設定を追加した。

```emacs-lisp
(leaf auctex
  :ensure t
  :hook
  (TeX-mode-hook . LaTeX-math-mode)
  (TeX-mode-hook . auto-image-file-mode)
  :init
  (setq org-preview-latex-default-process 'dvipng)
  (setq org-format-latex-options
        (plist-put org-format-latex-options :scale 1.5))
  :config
  (leaf latex-math-preview
    :ensure t
    :after auctex
    :config
    (setq latex-math-preview-in-math-mode-p-func 'latex-math-preview-in-math-mode-p
          latex-math-preview-tex-to-png-for-preview '(platex dvipng)
          latex-math-preview-tex-to-png-for-save '(platex dvipng)
          latex-math-preview-tex-to-eps-for-save '(platex dvips-to-eps)
          latex-math-preview-beamer-to-png '(platex dvipdfmx gs-to-png)))

  (leaf company-math
    :ensure t
    :hook (TeX-mode-hook . company-math-mode-setup)
    :config
    (defun company-math-mode-setup ()
      (require 'company-math)
      (setq-local company-backends
                  (append '((company-math-symbols-latex company-latex-commands))
                          company-backends))))
  ;; インラインプレビューの高速化
  (add-hook 'TeX-mode-hook (lambda () (setq preview-image-type 'dvipng)))
  ;; インラインプレビューの文字化け回避
  (add-hook 'TeX-mode-hook
            (lambda ()
              (setq preview-default-option-list
                    '("displaymath" "floats" "graphics" "textmath" "footnotes")))))
```

この設定で、OrgファイルにLaTeX形式で数式を書いたら、 `C-c C-x C-l` でプレビューできるようになった。
デフォルトではプレビュー文字が小さかったため、以下の設定で文字サイズを大きくしている。

```emacs-lisp
(setq org-preview-latex-default-process 'dvipng)
(setq org-format-latex-options
      (plist-put org-format-latex-options :scale 1.5))
```

いきなりOrgファイルに直接LaTeXを書くのは難しいので、[texlab](https://github.com/latex-lsp/texlab) というLaTeX用のLSPサーバを導入して
`.sty` ファイルでLSPのサポートを受けながら書いたものをOrgモードに写している。

```emacs-lisp
:hook
(go-ts-mode-hook . eglot-ensure)
(LaTeX-mode-hook . eglot-ensure)
:config
(add-to-list 'eglot-server-programs '(LaTeX-mode . ("texlab"))))
```

[こちら](https://note.com/9256/n/ne9cba9f6bcf5)を参考にして数式の書き方を覚えていきたい。


## 参考 {#参考}

-   [EmacsにおけるLaTeX執筆環境構築（１）AUCTeXの設定と使い方について](https://tam5917.hatenablog.com/entry/2021/03/30/202037#%E3%82%A4%E3%83%B3%E3%83%A9%E3%82%A4%E3%83%B3%E3%83%97%E3%83%AC%E3%83%93%E3%83%A5%E3%83%BC%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
-   [【見習いTeX使いのために】最初に覚えるコマンドまとめ](https://note.com/9256/n/ne9cba9f6bcf5)
