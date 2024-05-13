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
---

If you just want to build pages and deploy to other page hosts, you can use [Sphinx Builder][sphinx-builder].


  [sphinx-builder]: https://github.com/Kjuly/sphinx-builder

