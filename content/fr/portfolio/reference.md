---
title: "Références : Configurer MkDocs pour Technical Margins"
linkTitle: Références
weight: 40  
type: docs
---

## À propos de ce document

Ce document de référence est destiné aux contributeurs et administrateurs techniques du projet *Technical Margins*. Il fournit une vue d'ensemble structurée de toutes les options de configuration, des personnalisations et des outils utilisés dans le projet.

Utilisez-le pour :

- Comprendre rapidement l'architecture technique avant de faire des modifications.  
- Vérifier les paramètres exacts sans devoir fouiller dans les fichiers YAML, CSS ou Docker.  
- Vous assurer de la cohérence des changements apportés (par exemple, lors de l'ajout d'une langue, d'un plugin ou d'une fonction de CI/CD).  
- Accompagner vos déploiements, notamment en Docker ou via le pipeline CI/CD.

{{< alert title="À noter" color="info" >}}

Ce document n'a pas vocation à expliquer **pourquoi** certains choix ont été faits (voir les pages d'[explication](../explanation/)), ni à guider étape par étape (voir les [tutoriels](../tutorial/) et [guides pratiques](../guide/)). Il est conçu comme un point de référence consultable à tout moment.

{{< /alert >}}

## Aperçu des fichiers

| Fichier                     | Rôle principal                                     |
| --------------------------- | -------------------------------------------------- |
| `config/mkdocs.yml`         | Configuration de base (thème, plugins, extensions) |
| `config/en/mkdocs.yml`      | Spécifique à l'anglais (localisation, navigation)  |
| `config/fr/mkdocs.yml`      | Spécifique au français                             |
| `config/ja/mkdocs.yml`      | Spécifique au japonais                             |
| `config/zh-cn/mkdocs.yml`   | Spécifique au chinois simplifié                    |
| `config/zh-tw/mkdocs.yml`   | Spécifique au chinois traditionnel                 |
| `docs/index.html`           | Redirection automatique selon la langue            |
| `overrides/`                | Personnalisation du thème (HTML, CSS, JS)          |
| `docker/margins.Dockerfile` | Construction multilingue et déploiement Docker     |
| `.github/workflows/ci.yml`  | Pipeline CI/CD GitHub Actions                      |

## Configuration de base (`config/mkdocs.yml`)

### Informations projet

```yaml
site_name: 'Technical Margins'
site_author: The Margin Writer
use_directory_urls: true
```

### Validation

Configure les messages lors de `mkdocs serve` ou `mkdocs build` :

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

### Thème

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

### Extensions Markdown

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

Détails :

| Plugin      | Description                           |
| ----------- | ------------------------------------- |
| `blog`      | Articles, archives, catégories        |
| `tags`      | Gestion des étiquettes                |
| `search`    | Recherche multilingue avec filtrage   |
| `glightbox` | Visionneuse d'images                  |

## Organisation multilingue (`docs/`)

```
docs/
├── en/
├── fr/
├── ja/
├── zh-cn/
├── zh-tw/
├── 404.html         # Page 404 commune
├── index.html       # Redirection auto selon la langue
```

Exemple de redirection (`index.html`) :

``` js
if (language.startsWith("fr")) {
    window.location.href = "/material-margins/fr/index.html";
} else {
    window.location.href = "/material-margins/en/index.html";
}
```

## Configuration Docker (résumé)

| Étape   | Description                                          |
| ------- | ---------------------------------------------------- |
| Build   | Image MkDocs avec builds multilingues                |
| Serveur | Image Nginx pour servir le contenu                   |
| Proxy   | Image Nginx spéciale pour gérer `/material-margins/` |

Commandes principales :

``` bash
docker build -t technical-margins-site -f docker/margins.Dockerfile .
docker run -ti --rm --name material-margins -p 8082:80 technical-margins-site
docker build -t nginx-proxy-margins -f docker/nginx.Dockerfile .
docker run -ti --rm --name nginx-material-margins --link material-margins:material-margins -p 8083:80 nginx-proxy-margins
```

## CI/CD GitHub Actions

- Déclencheur : `push` sur `main`  
- Étapes :  

    - Build multilingue  
    - Copie des fichiers `index.html` et `404.html`  
    - Déploiement vers `gh-pages`  

## Commandes utiles

| Commande                                             | Description                   |
| ---------------------------------------------------- | ----------------------------- |
| `mkdocs serve -f config/en/mkdocs.yml`               | Dev anglais                   |
| `mkdocs serve -f config/fr/mkdocs.yml`               | Dev français                  |
| `mkdocs serve -f config/zh-cn/mkdocs.yml`            | Dev chinois simplifié         |
| `mkdocs serve -f config/zh-tw/mkdocs.yml`            | Dev chinois traditionnel      |
| `mkdocs serve -f config/ja/mkdocs.yml`               | Dev japonais                  |

## Voir aussi

- [MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Material Blog Plugin](https://squidfunk.github.io/mkdocs-material/plugins/blog/)
- [Docker](https://docs.docker.com/)
- [GitHub Pages](https://docs.github.com/en/pages)
