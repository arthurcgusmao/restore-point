# Restore Point

`restore-point-mode` is a global minor mode that allows you to restore the
point position after one or a sequence of specific commands were executed.

## Short Description

When the minor mode is active and you execute `keyboard-quit` (usually bound to
`C-g` or `ESC` keychords) after a sequence of mark or scroll commands (or any
other predefined set of commands of your choice, configurable in
`rp/restore-point-commands`), the point (cursor) position is restored to its
previous location.

## Installation & Usage

This package is going to be submitted to MELPA. Until then, please add
`restore-point.el` to your Emacs load path so that it can be required in your
initialization code.

Require package and enable the minor mode:

```lisp
(require 'restore-point)
(restore-point-mode 1)
```

### Further configurations

The package allows you to configure which functions are eligible to allow for
`keyboard-quit` to restore the point position after they are issued. By
default, *restore point* addresses the common scroll and mark commands that are
built-in to Emacs (please check the value of `rp/restore-point-commands` for
details.)

To modify the default commands, modify the list `rp/restore-point-commands` by
adding new commands (or completely setting its values to your liking), e.g.:

```lisp
(require 'restore-point)
;; Append these commands to restore-point commands list
(dolist (f '(er/mark-defun
             er/mark-paragraph
             er/mark-word))
  (add-to-list 'rp/restore-point-commands f t))
(restore-point-mode 1)
```

## Motivation

The functionality implemented herein is especially helpful when scroll commands
moved the point from where you had it in the first place, or if you mistakenly
executed some command (such as mark-whole-buffer) that moved the point position
and you want to restore it. Or, yet, if there is any command that moves the
point position that you want to be able to easily restore.

## Acknowledgements

The core idea of this package was firstly conceived and implemented by the
author alone as a custom function; however, the code herein was further
improved and refactored as a package by adapting code and ideas from
[`smart-mark.el`](https://github.com/zhangkaiyulw/smart-mark/blob/master/smart-mark.el),
a very similar package with similar purpose developed by Kai Yu.

