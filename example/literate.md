---
jupyter:
  kernelspec:
    display_name: Haskell
    language: haskell
    name: haskell
  language_info:
    codemirror_mode: ihaskell
    file_extension: .hs
    name: haskell
    pygments_lexer: Haskell
    version: 8.10.7
  nbformat: 4
  nbformat_minor: 4
title: Notebook title
---

# This is a Header

This is some code in Bird-style

``` {.haskell .literate}
func :: Int -> Int 
func = (+42)
```

This is a list using markdown regular syntax

-   One
-   Two
-   Three
-   Caramba

## This is a second-level header

This can be handle by pandoc, but ghci wont load this file because of
two different styles of code.

``` {.haskell .literate}
more = "code" `elem` ["different", "style"]
dont = "mix different style in one literate file."
```

### Quoteblock syntax

`inline code` wont generate a code cell

> Use "space + greater than" to write a quoteblock.

All `>` symbols in the first column are interpreted as `Haskell` code

``` {.haskell .literate}
this = "is haskell code"
```

> this a quoteblock. Notice there should be one space between haskell
> code and quoteblocks, otherwise everything is interpreted as a
> quoteblock.

As a rule of thumb always surround your haskell code with empty lines to
prevent a missmatch between Haskell and markdown syntax
