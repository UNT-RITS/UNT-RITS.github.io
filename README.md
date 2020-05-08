# UNT RITS Documentation Github Page

## Purpose

Friendly place to keep up to date documentations for **UNT HPC Talon**

## What we used

Main page present at [https://unt-rits.github.io/](https://unt-rits.github.io/) is built with [MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

Talon Standard Operating Procedure Guide present at [http://UNT-RITS.github.io/talon_sop/_build/html/index.html](http://UNT-RITS.github.io/talon_sop/_build/html/index.html) is build with [Jupyter Book](https://jupyterbook.org/intro.html)


## Maintanance

Use as current folder `UNT-RITS.github.io`:

* Build website and move files:
  ```bash
  mkdocs build --config-file website_project/mkdocs.yml
  cp -rf website_project/site/* .
  rm -rf website_project/site
  ```
  
* Build Jupyter-Book under `UNT-RiTS.github.io/talon_sop/_build/html`:

```bash
jupyter-book build talon_sop
```

* Push to GitHub:

```bash
git add --all
git commit -m "Updates to Website"
git push origin master
```


