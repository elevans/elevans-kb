# pandoc

## Install pandoc

Run the following bash command to install pandoc and latex support (needed for PDF writing).

```bash
$ sudo apt install pandoc texlive-latex-base texlive-fonts-recommended texlive-extra-utils texlive-latex-extra
```

## Markdown to PDF with pandoc

To convert `.md` files into `.pdf` files use the following bash command.

```bash
$ pandoc input.md -o output.pdf
```

By default, `pandoc` will produce a PDF with aggressive document margins. To create a `.pdf` with more reasonable margin size, modify the bash command
with `-V geometry:margins=1in` for 1 inch margins.

```bash
$ pandoc -V geometry:margin=1in input.md -o output.pdf
```
