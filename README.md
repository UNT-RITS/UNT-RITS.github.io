# UNT Research IT Service [RITS] Documentation Github Page

## [https://unt-rits.github.io](https://unt-rits.github.io)

## Purpose

Friendly place to keep up to date documentations for **UNT HPC Talon**

## What we used

Main page present at [https://unt-rits.github.io/](https://unt-rits.github.io/) is built with [MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).


## Updating Documentation

### Modifying Documentation

When modifying information, move to the **website_project** directory  

```bash
cd website_project
```

You can modify the **mkdocs.yml** file to change the configurations and settings for the page.

You can move to the **docs** directories that have all the files for the pages.

You can test the MkDoc pages by running:
```bash
mkdocs serve
```

This will build your current build of the website and host it on your local computer.
Then you can open a web browser and go to
```
http://127.0.0.1:8000/
```

This is display your current website build so you can review it before you push it to github.

### Building website

When you are finishing modifing the webpages, then you need to build the website

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


