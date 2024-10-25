+++
title = "Copilot"
author = ["wtnbjn"]
tags = ["Emacs", "Reference"]
draft = false
+++

-   `s-p` でcopilotモード起動
-   `Tab` で補完の選択
-   `C-c Tab` で次の補完

とした。copilot-chatも導入して、特に問題なく動いているが、現時点で使用する場面がはっきりしていない。

```emacs-lisp
(leaf copilot
  :el-get (copilot
           :type github
           :pkgname "zerolfx/copilot.el")
  :bind
  ("s-p" . copilot-mode)
  :config
  (leaf editorconfig :ensure t)
  (leaf s :ensure t)
  (leaf dash :ensure t)
  (defun my/copilot-tab ()
    (interactive)
    (or (copilot-accept-completion)
        (indent-for-tab-command)))
  (with-eval-after-load 'copilot
    (define-key copilot-mode-map (kbd "<tab>") #'my/copilot-tab)
    (define-key copilot-mode-map (kbd "C-c <tab>") #'copilot-next-completion)))

(leaf copilot-chat
  :el-get (copilot-chat :type github :pkgname "chep/copilot-chat.el")
  :after (request shell-maker)
  :custom
  (copilot-chat-frontend 'shell-maker)
  :config
  (require 'copilot-chat-shell-maker)
  (push '(shell-maker . copilot-chat-shell-maker-init) copilot-chat-frontend-list)
  (copilot-chat-shell-maker-init))
```
