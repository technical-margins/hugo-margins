---
title: "Tutoriel : Créez votre premier article de blog"
linkTitle: "Créer votre premier article"
weight: 10  
type: docs
---

Ce tutoriel vous guide dans la rédaction et la publication de votre premier article sur le blog *Technical Margins*. À la fin, vous aurez écrit, structuré et publié un article contenant des métadonnées, des images et une structure correcte.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

- [Python](https://www.python.org/downloads) (version 3.12 recommandée)  
- [Git](https://git-scm.com/downloads)  
- Un compte [GitHub](https://github.com/)  
- Des bases de [Markdown](https://www.markdownguide.org/)  
- Un éditeur de texte, par ex. [VS Code](https://code.visualstudio.com/download)  

{{< alert title="Conseil" >}}
Extensions VS Code recommandées :
- **Python** (Microsoft)  
- **Markdownlint** (pour faciliter l’édition)  
{{< /alert >}}

Accès requis au dépôt GitHub : `technical-margins/material-margins`

## Étape 1 : Cloner le dépôt

1. Ouvrez l’explorateur de fichiers.
2. Allez dans le dossier de votre choix, ex. `Documents/MesProjets`
3. Faites clic droit puis :

   - Linux : *Ouvrir dans un terminal*
   - Windows : *Ouvrir dans PowerShell*
   - macOS : *Nouveau terminal au dossier*

4. Exécutez :

    ```bash
    git clone https://github.com/technical-margins/material-margins.git
    ```

5. Ouvrez VS Code, sélectionnez le dossier `material-margins`.

6. Vous devriez voir :
   - `requirements.txt`
   - `config/`
   - `docs/`
   - `overrides/`

{{< alert title="Utilisateurs avancés" >}}
Depuis le terminal :

```bash
cd /chemin/du/dossier
git clone https://github.com/technical-margins/material-margins.git
cd material-margins
code .
```

Assurez-vous que la commande `code` est dans votre PATH.
{{< /alert >}}

## Étape 2 : Préparer votre environnement

1. Dans VS Code : *Terminal > Nouveau terminal*

2. Créez un environnement virtuel :

   ```bash
   python -m venv .venv
   ```

3. Activez-le :

   * macOS/Linux :

     ```bash
     source .venv/bin/activate
     ```

   * Windows (PowerShell) :

     ```powershell
     .venv\Scripts\Activate.ps1
     ```

4. Vérifiez la présence du préfixe `(.venv)` dans le terminal.

5. Installez les dépendances :

   ```bash
   pip install -r requirements.txt
   ```

{{< alert title="Méthode alternative CLI" >}}

Depuis le terminal :

```bash
cd material-margins
python -m venv .venv
source .venv/bin/activate  # Windows : .venv\Scripts\activate
pip install -r requirements.txt
code .
```

{{< /alert >}}

## Étape 3 : Créer le fichier d’article

1. Dans VS Code, allez dans `docs/fr/blog/posts/`
2. Clic droit → *Nouveau fichier* → `mon-premier-article.md`

{{< alert title="Méthode alternative CLI" >}}

Depuis le terminal :

```bash
touch docs/fr/blog/posts/mon-premier-article.md
```

{{< /alert >}}

## Étape 4 : Ajouter les métadonnées et le contenu

Dans `mon-premier-article.md` :

```markdown
---
date:
  created: 2025-05-07
comments: true
authors:
  - TheMarginWriter
slug: mon-premier-article
categories:
  - Réflexions personnelles
tags:
  - Apprentissage
  - MkDocs
  - Tutoriel
---

# Mon premier article sur Technical Margins

Ceci est mon premier article sur *Technical Margins*. J’y partage...

<!-- more -->

## Introduction

Introduction ici...

## Partie principale

Le contenu principal ici...

<figure markdown="1">
![Texte alternatif](https://example.com/chemin/vers/image.jpg)
</figure>

## Conclusion

Conclusion ici...
```

* Utilisez des **URL absolues** pour les images.
* Le champ `slug` détermine le segment final de l’URL.
* Le `<!-- more -->` sert à découper l’aperçu du billet sur la page de liste.

{{< alert title="Structure multilingue" >}}
Emplacement du fichier selon la langue :

* Français : `docs/fr/blog/posts/`
* Anglais : `docs/en/blog/posts/`
* Chinois simplifié : `docs/zh-cn/blog/posts/`
* Chinois traditionnel : `docs/zh-tw/blog/posts/`
* Japonais : `docs/ja/blog/posts/`
  {{< /alert >}}

## Étape 5 : Prévisualiser l’article

1. Assurez-vous que l’environnement `(.venv)` est actif.

2. Exécutez :

   ```bash
   mkdocs serve -f config/fr/mkdocs.yml
   ```

3. Accédez à [http://localhost:8000/](http://localhost:8000/)

{{< alert title="Changer de langue" >}}
Pour prévisualiser une autre langue :

```bash
mkdocs serve -f config/en/mkdocs.yml
```

{{< /alert >}}

## Étape 6 : Commiter et pousser

```bash
git add docs/fr/blog/posts/mon-premier-article.md
git commit -m "Ajout de mon premier article"
git push origin main
```

## Étape 7 : Vérification en ligne

Allez sur :

```
https://technical-margins.github.io/material-margins/
```

L’article devrait apparaître dans *Blog*.

{{< alert title="Redirection multilingue" >}}
Le `index.html` principal redirige automatiquement vers `/fr/`, `/en/`, etc., selon la langue du navigateur.
{{< /alert >}}

## Et ensuite ?

Essayez :

* [Des tableaux](https://squidfunk.github.io/mkdocs-material/reference/data-tables/)
* [Des blocs de code](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/)
* [Des admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/)
