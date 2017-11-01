# Emacs

## Create Init File

Simply create a file called `~/.emacs` and you're good to go.

## Auto Save Files

By default, emacs creates `filename~` files in the same directory as the original file as auto-save files in case you wish to recover from a crash. This can clutter your filesystem tree pretty quickly and thus it is recommended to put them in a separate directory which emacs is aware of.

I use `~/.emacs_saves`:

```
;; auto save directory
(setq backup-directory-alist
          `((".*" . ,"~/.emacs_saves")))
    (setq auto-save-file-name-transforms
          `((".*" ,"~/.emacs_saves" t)))

```

## MELPA Packages

[MELPA](https://melpa.org/#/) is a very cool package manager for emacs. Highly recommended.

To install, open your init file and enter:

```
;; packages
(when (>= emacs-major-version 24)
  (require 'package)
  (package-initialize)
  (add-to-list 'package-archives '("melpa" . "http://melpa.milkbox.net/packages/") t)
  )
```

## Emacs Theme

The theme I prefer is `dakrone`.

To install, simply run

```
M-x package-install RET dakrone-theme
M-x customize-themes -> Select dakrone with RET and type 'y' for both questions
```