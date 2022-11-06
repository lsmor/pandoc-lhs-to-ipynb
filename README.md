# Literate Haskell to Jupyter Notebook

This is a very small lua filter which allows conversion from literate haskell files to notebooks. Use the follwing command:

```bash
#                |- set the source style as markdown with literate haskell rules
#                |                 |- set target style as a jupter notebook
#                |                 |                  |- tell pandoc to use this lua filter. Pandoc includes a lua interpreter, so no need to extra deps.
#                |                 |                  |                           |- output file path
#                |                 |                  |                           |                    |- input file path
pandoc -s --from markdown+lhs --to ipynb --lua-filter path/to/lhs-to-ipynb.lua -o path/to/output.ipynb path/to/input.lhs 
```

This filter is so simple that probably can be achive with a command line option, but I am too lazy to investigate it

## Syntactic considerations

Literate comments should be written in markdown style with the following conventions:

- Use a `yaml` header to specify `ihaskell` kernel
- Markdown headers should be marked with `=` instead of `#` because hashtag is interpreted by haskell compiler as [number line token](https://pandoc.org/MANUAL.html#extension-literate_haskell)
- Haskell code can be introduced either by `>` or in between `begin{code} ... \end{code}` following [haskell report](https://www.haskell.org/onlinereport/literate.html)
- Notice that both styles are valid for `pandoc` even if they are mixed within the same `lhs` file, but `ghci` wont load mixed style code.
- Markdown's quoteblocks syntax collapse with Bird-style `literate Haskell` as symbol `>` is used by both of them.
- Luckily `ghc` interprets `>` as `Haskell` code, if and only if `>` is in the first column, so use `[space]>` to write a markdown quoteblock.
- Always surround `Haskell` code by blank lines. This is not required by either `ghc` nor `pandoc` but it might cause some undesired edge cases: for example a quoteblock followed by `haskell` code is wrongly interpreted as a single quoteblock.

In folder [example](./example) you can find a literate haskell file [literate.hls](./example/literate.hls) and the corresponding jupyter notebook generated with pandoc
