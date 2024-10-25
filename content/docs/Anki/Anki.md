+++
title = "Anki"
author = ["wtnbjn"]
tags = ["Anki", "Reference"]
draft = false
+++

## Setup {#setup}


### Anki {#anki}

まずは、Ankiを[こちら](https://apps.ankiweb.net/)からダウンロードしてインストールします。


### Anki Connect {#anki-connect}

OrgファイルとAnkiを連携するためには、Ankiアプリに [Anki Connect](https://foosoft.net/projects/anki-connect/)というプラグインをインストールする必要があります。
プラグインのインストール後、Ankiアプリを再起動してください。


### Emacs {#emacs}

`init.el` に以下のコードを追加し、 `anki-editor` の設定を行いました。

```emacs-lisp
(leaf anki-editor
  :doc "Minor mode for working with Anki decks and notes."
  :url "https://github.com/louietan/anki-editor"
  :ensure t
  :bind
  ((:anki-editor-mode-map
    ("C-c a" . anki-editor/body)))
  :pretty-hydra
  ((:title "Anki Editor" :color blue :quit-key "q" :foreign-keys warn :separator "╌")
   ("Main"
    (("p" anki-editor-push-notes              "push notes")
     ("n" anki-editor-push-new-notes          "push new notes")
     ("r" anki-editor-retry-failed-notes      "retry failed notes"))
    "Editing"
    (("i" anki-editor-insert-default-note     "insert default")
     ("I" anki-editor-insert-note             "insert note")
     ("d" anki-editor-delete-notes            "delete note")
     ("c" anki-editor-cloze-dwim              "cloze region or word"))
    "Export"
    (("e" anki-editor-export-subtree-to-html  "export subtree to HTML")
     ("h" anki-editor-convert-region-to-html  "convert region to HTML"))
    "Other"
    (("a" anki-editor-api-check               "API check")
     ("s" anki-editor-sync-collections        "sync collections")
     ("b" anki-editor-gui-browse              "browse in GUI")
     ("g" anki-editor-gui-add-cards           "add cards in GUI")))))
```

READMEに載ってるコマンドをChatGPTに貼り付けて、pretty-hydra化した。


## コマンド {#コマンド}


### anki-editor-insert-note {#anki-editor-insert-note}

ノート作成用コマンドです。以下の手順でノートが作成されます。

1.  デッキの選択
2.  ノートタイプの選択
3.  ノートの見出し(Note Heading)の入力

上記を入力すると、Anki用の `PROPERTIES` が付与されたOrgエントリが挿入されます。
挿入時点ではAnki側には送信されないため、送信は別途 `anki-editor-push-notes` コマンドで行います。

{{< figure src="/ox-hugo/ezgif-5-27ada701ba.gif" >}}

なお、デッキはOrgファイルのプロパティや、親のサブツリーに設定がある場合は継承されるので、
コマンド実行時に入力する必要はありません。
また、anki-editorは、READMEに記載されているようにBack/Front用のサブツリーを省略した簡易的な書き方もサポートしています。
この形式を使用したい場合は、Note Headingを空欄にしておくと自動でサブツリーが作成されません。


### anki-editor-insert-default-note {#anki-editor-insert-default-note}

このノート作成コマンドは、Orgファイルのプロパティや親のサブツリーで設定した `ANKI_DEFAULT_NOTE_TYPE` を自動で読み込み、
ノートタイプを決定します。
私の運用では、1つのOrgファイルにつき1つのデッキとノートタイプのみを使用しているため、
Orgファイルのプロパティに `ANKI_DECK` と `ANKI_DEFAULT_NOTE_TYPE` を設定し、
このコマンドを使ってノートを追加するようにしています。


### anki-editor-push-notes {#anki-editor-push-notes}

作成したノートをAnkiアプリに送信するためのコマンドです。
Ankiアプリが起動中で、かつAnki Connect設定済みである必要があります。

送信後、エントリにANKI_NOTE_IDが付与され、次回以降の更新が可能になります。

```org
:PROPERTIES:
:ANKI_NOTE_TYPE: Basic
:ANKI_DECK: English
:ANKI_NOTE_ID: 1729834505855
:END:
```


### anki-editor-push-new-notes {#anki-editor-push-new-notes}

まだAnkiに送信していないノートを送信します。


### anki-editor-cloze-dwim {#anki-editor-cloze-dwim}

択したリージョンまたはカーソル下の単語をAnkiの穴埋め問題形式に変換します。
穴埋め問題については[こちら](https://rs.luminousspice.com/cloze-deletion/)が分かりやすいです。


### anki-editor-gui-browse {#anki-editor-gui-browse}

カーソル位置のノートをAnkiアプリで確認できます。
