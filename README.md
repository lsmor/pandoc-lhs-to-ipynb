# Literate Haskell to Jupyter Notebook

This repository contains a few examples on how to convert Literate Haskell files to other formats. It includes a very small lua filter which allows conversion from Literate Haskell files to jupyter notebooks.

```bash
pandoc -s \
       --from markdown+lhs \                   # set the source style as markdown with Literate Haskell rules
       --to ipynb \                            # set target style as a jupter notebook
       --lua-filter path/to/lhs-to-ipynb.lua \ # tell pandoc to use this lua filter. Pandoc includes a lua interpreter, so no need to extra deps.
       -o path/to/output.ipynb \               # output file path
       path/to/input.lhs                       # intput file path
```

This filter is so simple that probably can be achive with a command line option, but I am too lazy to investigate it

## Other styles

For output format can be other than `ipynb` don't use this filter, as it will prevent code style. In example folder there are [markdown](./example/literate.md) and [html](example/literate.html) outputs generated with

- lhs to regular markdown

```bash
# Force atx header to avoid underliying level 1 and two headers
pandoc -s --markdown-headings=atx --from markdown+lhs --to markdown -o example/literate.md example/literate.lhs
```

- lhs to html

```bash
pandoc -s --from markdown+lhs --to html -o example/literate.html example/literate.lhs
```

## Syntactic considerations

Literate comments should be written in markdown style with the following conventions:

- Use a `yaml` header to specify `ihaskell` kernel
- Markdown headers should be marked with `=` instead of `#` because hashtag is interpreted by haskell compiler as [number line token](https://pandoc.org/MANUAL.html#extension-literate_haskell)
- Haskell code can be introduced either by `>` or in between `begin{code} ... \end{code}` following [haskell report](https://www.haskell.org/onlinereport/literate.html)
- Notice that both styles are valid for `pandoc` even if they are mixed within the same `lhs` file, but `ghci` wont load mixed style code.
- Markdown's quoteblocks syntax collapse with Bird-style `Literate Haskell` as symbol `>` is used by both of them.
- Luckily `ghc` interprets `>` as `Haskell` code, if and only if `>` is in the first column, so use `[space]>` to write a markdown quoteblock.
- Always surround `Haskell` code by blank lines. This is not required by either `ghc` nor `pandoc` but it might cause some undesired edge cases: for example a quoteblock followed by `haskell` code is wrongly interpreted as a single quoteblock.

In folder [example](./example) you can find a Literate Haskell file [literate.lhs](./example/literate.lhs) and the corresponding jupyter notebook generated with pandoc

## Hakyll Integration

The main purpose of this repo is to serve as example on `markdown + lhs` files as I couldn't find good/updated info about it on internet. `Hakyll` is capable of reading and compiling Literate Haskell files using the standard `Hakyll.pandocCompiler` converting them into html. This makes Literate Haskell files a good candidate for writing and sharing your Haskell blogs.