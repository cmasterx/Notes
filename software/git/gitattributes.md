# Git Attributes
The Git Attributes file (`.gitattributes`) allows git to treat certain files and/or file types differently to handle os-dependent end-of-line behavior for text files, enforce end-of-line behavior across platforms, and configure git to parse/diff certain files or file types in a different format.

# End-of-Line
End-of-Line (**EOL**) can be configured by adding the following to the `.gitattributes` file:

``` text
*.txt text
*.sh  text eol=lf    # force LF newlines on GNU+Linux shell scripts
*.bat text eol=crlf  # force CRLF newlines on Windows batch files
*.jpg -text          # JPG files are not text
*.png -diff          # PNG files cannot be diffed
*.gif -text -diff -merge # GIF files are not text, cannot be diffed and cannot be merged
*.ogg binary         # equivalent to -text -diff -merge
```
[[source - refer: _Stack Overflow - EOL_](https://stackoverflow.com/questions/73853086/what-is-the-point-of-using-gitattributes-file)]

# Parsing
Git can be configured to parse non-text files by passing the file to a parser.

## Microsoft Office Documents
`.gitattributes`:
```
*.doc diff=word
*.xsl diff=excel
*.xlsx diff=zip
*.docx diff=zip
```

`.gitconfig`:
``` text
[diff "zip"]
[diff "word"] 
    textconv = strings
[diff "excel"]
    textconv = strings
[diff "zip"]
    textconv = unzip -c -a
```
[[source](#references) - refer: _Stack Overflow - Word Documents_]

# References
- [Stack Overflow - EOL](https://stackoverflow.com/questions/73853086/what-is-the-point-of-using-gitattributes-file)
- [Stack Overflow - Word Documents](https://stackoverflow.com/questions/22439517/view-docx-file-on-github-and-use-git-diff-on-docx-file-format)