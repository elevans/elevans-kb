# elevans-kb
This repository hosts information (a knowledge base) on how to do things that I've figured out.

To build the docs, pull this repository and construct a conda/mamba environment using the `environment.yml` file in this repository.

```bash
$ mamba env create -f environment.yml -n docs
```

Then navigate the `docs` folder and build the docs with:

```bash
$ make clean html
```

You can view the knowledge base by opening `index.html` in a web browser.
