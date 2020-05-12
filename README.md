# UNT Research IT Service [RITS] Documentation Github Page

## [https://unt-rits.github.io](https://unt-rits.github.io)

## Purpose

Friendly place to keep up to date documentations for **UNT HPC Talon**

## What we used

Main page present at [https://unt-rits.github.io/](https://unt-rits.github.io/) is built with [MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).


## Maintanance

Use as current folder `UNT-RITS.github.io`:

* Build website and move files:
  ```bash
  mkdocs build --config-file website_project/mkdocs.yml
  cp -rf website_project/site/* .
  rm -rf website_project/site
  ```

* Push to GitHub:

  ```bash
  git add --all
  git commit -m "Updates to Website"
  git push origin master
  ```


