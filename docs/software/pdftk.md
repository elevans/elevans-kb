# pdftk

## Combine PDFs

To combine two PDFs use the following `pdftk` command:

```bash
$ pdftk file_1.pdf file_2.pdf cat output merged.pdf
```

## Split PDFs

To split PDFs into multiple documents use the following `pdftk` command:

```bash
$ pdftk merged.pdf cat 1-4 output split.pdf
```

Where `1-4` referes to the pages to split into the `split.pdf` output document.