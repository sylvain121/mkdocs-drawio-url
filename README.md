# MkDocs Plugin for embedding Drawio files with url

[Buy Sergey a ☕](https://www.buymeacoffee.com/SergeyLukin) 

Sergey ([onixpro](https://github.com/onixpro)) is the original creator of this plugin. Repo can be found [here.](https://github.com/onixpro/mkdocs-drawio-file)

## Features
This plugin enables you to embed interactive drawio diagrams in your documentation. Simply add your diagrams like you would any other image:

```markdown
![](my-diagram.drawio)
![](../other-diagram.drawio)
```

## Setup

Install plugin using pip:

```
pip install mkdocs-drawio-url
```

Add the plugin to your `mkdocs.yml`

```yaml
plugins:
  - drawio-url
```

### Configuration

By default the plugin uses the official url for the minified drawio javascript library. To use a custom source for the drawio viewer you can overwritte the url. This might be useful in airlocked environments.

> If you want to use a self-hosted JavaScript viewer file. You should download the latest version from the [official drawio repo](https://github.com/jgraph/drawio/blob/dev/src/main/webapp/js/viewer-static.min.js).

```yaml
plugins:
  - drawio-url:
      viewer_js: "https://viewer.diagrams.net/js/viewer-static.min.js"
```

## How it works

1. mkdocs generates the html per page
2. `mkdocs-drawio-url` attaches to the `on_post_page` event. For more details, please have a look at the [event lifecycle documentation](https://www.mkdocs.org/dev-guide/plugins/#events)
3. Adds the drawio viewer library
4. Searches through the generated html for all `img` tags that have a source of type `.drawio`
5. Replaces the found `img` tags with `mxgraph` html blocks (actual drawio diagram content). For more details, please have a look at the [official drawio.com documentation](https://www.drawio.com/doc/faq/embed-html).


## Contribution guide

1. Either use the devcontainer or setup a venv with mkdocs installed
2. Install your current local version: `pip install -e .`
3. Add a test for your changes in the `example` directory
4. Test your changes by starting `mkdocs serve` in the `example` directory
5. Increase the version `pyproject.toml` and `setup.py`
6. Open pull request
