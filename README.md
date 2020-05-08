# UNT RITS Documentation Github Page

## Currently built with `mkdocs` and `jupyter-book`

## How to maintain it:

Make changes to main pages that are built with `MkDoc`:

Use as current folder `UNT-RiTS.github.io`

Build website and move files:
  ```bash
  mkdocs build --config-file website_project/mkdocs.yml
  cp -rf website_project/site/* .
  rm -rf website_project/site
  ```
  
Build Jupyter-Book under `UNT-RiTS.github.io/talon_sop/_build/html`:

```bash
jupyter-book build talon_sop
```

Push to GitHub:

```bash
git add --all
git commit -m "Updates to Website"
git push origin master
```

