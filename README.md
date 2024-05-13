# sphinx-publisher
Github Action to deploy Sphinx source files as Github Pages.

## Configurations

| Input | Default | Description
| --- | --- | ---
| source_root | docs/source | Root directory of source to build.
| build_root | docs/build | Root directory for build output.
| default_lang | en | The default language, which will be placed under the build directory, no subdirectory will be created.
| lang_mappings | '' | Newline-separated list of folder & language mappings to build (refer to [Multiple languages](#multiple-languages). If you don't provide one, will use Makefile's SOURCEDIR & BUILDDIR to determine.

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
```sh
/docs
    /source
    /build
```

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
```sh
/docs
    /source
        /en
        /zh-Hans
    /build
```

## Share & Override Config File

You can provide `_conf.py` to share and override `conf.py`. Below is a sample folder structure:

```sh
/source
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

