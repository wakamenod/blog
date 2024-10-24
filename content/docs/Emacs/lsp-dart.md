+++
title = "lsp-dart"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = false
+++

久し振りにFlutterプロジェクトを開いたら、動かなくなってて困った。
前回からEmacsの設定を大幅な見直しがあったので、それが要因だと思うけど、結局根本的な原因はよく分からず...

以前はlsp-dartを入れるだけで大体動いたと記憶してるが、今回はシンタックスハイライトが効かなかったり、LSPが起動しなくなったり嵌ってしまった。

```dart
(leaf dart-mode
  :ensure t
  :init
  (require 'tree-sitter)
  (require 'treesit)
  (add-hook 'dart-mode-hook #'tree-sitter-hl-mode)
  :mode (("\\.dart\\'" . dart-mode)))
(leaf lsp-dart
  :ensure t
  :config
  (defun wal/find-dart-flutter-sdk-dir ()
    "Find the Dart Flutter SDK directory."
    (when-let* ((flutter-bin (executable-find "flutter"))
                (sdk-dir (string-trim (shell-command-to-string "flutter sdk-path"))))
      sdk-dir))
  (setq lsp-dart-test-tree-on-run nil)
  (when (string= system-type "gnu/linux")
    (setq lsp-dart-flutter-sdk-dir (wal/find-dart-flutter-sdk-dir)))
  (when (string= system-type "darwin")
    (setq lsp-dart-flutter-sdk-dir "~/flutter"))
  (when (string= system-type "windows-nt")
    (setq lsp-dart-flutter-sdk-dir "C:/Users/wtnbjn/scoop/apps/flutter/current"))
  :custom
  (lsp-dart-test-tree-on-run . nil)
  :hook (dart-mode-hook . lsp))
```

以下のとおり、 `dart-mode` でtree-sitter-hl-modeをフックするようにした。

```emacs-lisp
:init
(require 'tree-sitter)
(require 'treesit)
(add-hook 'dart-mode-hook #'tree-sitter-hl-mode)
:mode (("\\.dart\\'" . dart-mode)))
```

こんなの前までやらなくてもハイライトされてたと思うんだけど、謎。

[dar-ts-mode](https://github.com/50ways2sayhard/dart-ts-mode) を用意してくれてる方がいて、セットアップすると `ts-mode` になるのでハイライトされるが、
今度はlsp-dartでlspが起動しなくなってしまう。 多分、lsp-dartがまだdart-mode前提になってる。
