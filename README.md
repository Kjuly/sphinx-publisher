# sphinx-publisher
Github Action to deploy Sphinx source files as Github Pages.

## Usage

### One language only

```yaml
# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  publish:
    name: Publish Sphinx Pages
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Publish Pages
        id: deployment
        uses: Kjuly/sphinx-publisher@main
```

Folder structure:
> /src  
> /build

### Multiple languages

```yaml
...
uses: Kjuly/sphinx-publisher@main
with:
  default_lang: en
  lang_mappings: |-
    en:en
    zh-Hans:zh_CN
```

Folder structure:
> /src  
> -- /en  
> -- /zh-Hans  
> /build  

## Share & Override Config File

You can provide `_conf.py` to share and override `conf.py`. Below is a sample folder structure:

```sh
/src  
    _conf.py  # Shared base config file.

    /en  
        _conf.py  # Override config file for "en".  
        conf.py   # The final generated config file for "en", which will be updated for each build process.
        ...       #   You don't need to provide it manually.

    /zh-Hans  
        conf.py   # No "_conf.py" provided at the same level, will use "conf.py" as it was.
        ...
/build  
```

---

If you just want to build pages and deploy to other page hosts, you can use [Sphinx Builder][sphinx-builder].


  [sphinx-builder]: https://github.com/Kjuly/sphinx-builder

