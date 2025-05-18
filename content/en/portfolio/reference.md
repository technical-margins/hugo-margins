---
title: "Reference: Configuring Technical Margins MkDocs"
linkTitle: Reference
weight: 40  
type: docs
---

## About this document

This reference document is intended for contributors and technical administrators of the *Technical Margins* project. It provides a structured overview of all configuration options, customisations and tools used in the project.

Use it to:

- Quickly understand the technical architecture before making changes.  
- Check exact parameters without having to dig through YAML, CSS or Docker files.  
- Ensure consistency of changes made (for example, when adding a language, plugin or CI/CD function).  
- Support your deployments, particularly in Docker or via the CI/CD pipeline.

{{< alert name="Please note" color="info" >}}

This document is not intended to explain **why** certain choices were made (see the [explanation](../explanation/) pages), nor to provide step-by-step guidance (see the [tutorials](../tutorial/) and [how-to guides](../guide/)). It is designed as a reference point that can be consulted at any time.

{{< /alert >}}

## Files overview

| File                          | Main role                                       |
| ----------------------------- | ----------------------------------------------- |
| `config/mkdocs.yml`           | Base configuration (theme, plugins, extensions) |
| `config/en/mkdocs.yml`        | English-specific (localisation, navigation)     |
| `config/fr/mkdocs.yml`        | French-specific                                 |
| `config/ja/mkdocs.yml`        | Japanese-specific                               |
| `config/zh-cn/mkdocs.yml`     | Simplified Chinese-specific                     |
| `config/zh-tw/mkdocs.yml`     | Traditional Chinese-specific                    |
| `docs/index.html`             | Automatic redirection based on language         |
| `overrides/`                  | Theme customisation (HTML, CSS, JS)             |
| `docker/margins.Dockerfile`   | Multilingual build and Docker deployment        |
| `.github/workflows/ci.yml`    | GitHub Actions CI/CD pipeline                   |

## Base configuration (`config/mkdocs.yml`)

### Project information

```yaml
site_name: 'Technical Margins'
site_author: The Margin Writer
use_directory_urls: true
```

### Validation

Configures messages during `mkdocs serve` or `mkdocs build`:

```yaml
validation:
  nav:
    omitted_files: info
    not_found: warn
    absolute_links: info
  links:
    not_found: warn
    anchors: info
    absolute_links: info
    unrecognized_links: info
```

### Theme

```yaml
theme:
  name: material
  favicon: assets/images/favicon.ico
  custom_dir: '../../overrides/'
  palette:
    - scheme: margin
      primary: custom
      accent: custom
      toggle:
        icon: material/weather-night
    - scheme: slate
      primary: custom
      accent: custom
      toggle:
        icon: material/weather-hazy
  font:
    text: Nunito
    code: Roboto Mono
  icon:
    logo: fontawesome/solid/pen-nib
    menu: material/microsoft-xbox-controller-menu
    previous: material/skip-previous-outline
    next: material/skip-next-outline
    alternate: material/translate-variant
    admonition:
      example: material/tooltip-edit-outline
      note: material/pin-outline
      abstract: material/eye-outline
      info: material/information-outline
      tip: material/star-circle-outline
      success: material/check-circle-outline
      question: material/help-circle-outline
      warning: material/alert-circle-outline
      failure: material/close-circle-outline
      danger: material/radioactive-circle-outline
      bug: material/bell-circle-outline
      quote: material/comma-circle-outline
  features:
    - navigation.footer
    - navigation.indexes
    - navigation.sections
    - navigation.tabs
    - navigation.top
    - toc.follow
    - content.code.copy
```

### Markdown extensions

```yaml
markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.highlight
  - pymdownx.inlinehilite
  - pymdownx.superfences
  - pymdownx.snippets
  - attr_list
  - md_in_html
  - pymdownx.emoji
  - pymdownx.tabbed
  - pymdownx.arithmatex
```

### Plugins

```yaml
plugins:
  - blog
  - tags
  - search
  - glightbox
```

Details:

| Plugin      | Description                          |
| ----------- | ------------------------------------ |
| `blog`      | Articles, archives, categories       |
| `tags`      | Tag management                       |
| `search`    | Multilingual search with filtering   |
| `glightbox` | Image viewer                         |

## Multilingual organisation (`docs/`)

```
docs/
├── en/
├── fr/
├── ja/
├── zh-cn/
├── zh-tw/
├── 404.html         # Common 404 page
├── index.html       # Auto redirection based on language
```

Redirection example (`index.html`):

```js
if (language.startsWith("fr")) {
    window.location.href = "/material-margins/fr/index.html";
} else {
    window.location.href = "/material-margins/en/index.html";
}
```

## Docker configuration (summary)

| Step    | Description                                          |
| ------- | ---------------------------------------------------- |
| Build   | MkDocs image with multilingual builds                |
| Server  | Nginx image to serve content                         |
| Proxy   | Special Nginx image to handle `/material-margins/`   |

Main commands:

```bash
docker build -t technical-margins-site -f docker/margins.Dockerfile .
docker run -ti --rm --name material-margins -p 8082:80 technical-margins-site
docker build -t nginx-proxy-margins -f docker/nginx.Dockerfile .
docker run -ti --rm --name nginx-material-margins --link material-margins:material-margins -p 8083:80 nginx-proxy-margins
```

## CI/CD GitHub Actions

- Trigger: `push` to `main`  
- Steps:  
  - Multilingual build  
  - Copy of `index.html` and `404.html` files  
  - Deployment to `gh-pages`  

## Useful commands

| Command                                              | Description                       |
| ---------------------------------------------------- | --------------------------------- |
| `mkdocs serve -f config/en/mkdocs.yml`               | English development               |
| `mkdocs serve -f config/fr/mkdocs.yml`               | French development                |
| `mkdocs serve -f config/zh-cn/mkdocs.yml`            | Chinese (simplified) development  |
| `mkdocs serve -f config/zh-tw/mkdocs.yml`            | Chinese (traditional) development |
| `mkdocs serve -f config/ja/mkdocs.yml`               | Japanese development              |

## See also

- [MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Material Blog Plugin](https://squidfunk.github.io/mkdocs-material/plugins/blog/)
- [Docker](https://docs.docker.com/)
- [GitHub Pages](https://docs.github.com/en/pages)
