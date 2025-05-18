---
title: "Tutoriel : Créez votre premier article de blog"
linkTitle: "Tutoriel"
weight: 10  
type: docs
---

Ce tutoriel vous guide pour rédiger et publier votre premier article sur le blog MkDocs Material *Technical Margins*. À la fin, vous aurez rédigé, mis en forme et publié un article avec des métadonnées, des images et une bonne structuration.

## Prérequis

Avant de commencer, assurez-vous d'avoir :

- [Python](https://www.python.org/downloads/) installé sur votre ordinateur (version 3.12 recommandée)  
- [Git](https://git-scm.com/downloads) installé  
- Un compte [GitHub](https://github.com/)  
- Des bases en syntaxe [Markdown](https://www.markdownguide.org/)  
- Un éditeur de texte ([VS Code](https://code.visualstudio.com/download) recommandé)  
- Un accès au dépôt GitHub : `technical-margins/material-margins` (🔒 privé)

{{< alert title="Extensions recommandées pour VS Code" color="success" >}}

- **Python** (Microsoft)  
- **Markdownlint** (pour le confort d'édition)  

{{< /alert >}}

## Étape 1 : Cloner le dépôt

Vous allez récupérer une copie locale du projet pour pouvoir travailler sur votre ordinateur et non directement en ligne.

1. Ouvrez votre explorateur de fichiers (Windows, Finder, ou autre).

2. Allez à l'endroit où vous voulez cloner le projet, par exemple `Documents`.

3. Créez un dossier, par exemple `MesProjets`.

4. Faites un clic droit sur ce dossier et sélectionnez :

    - sous Linux : *Ouvrir dans un terminal*  
    - sous Windows : *Ouvrir dans Terminal* ou *Ouvrir dans PowerShell*  
    - sous macOS : *Nouveau terminal au dossier* (via *Finder > Services* ; à activer si nécessaire dans les Préférences système)  

5. Clonez le dépôt en saisissant la commande :

    ``` bash
    git clone https://github.com/technical-margins/material-margins.git
    ```

6. Ouvrez VS Code et sélectionnez :
   *Fichier > Ouvrir dossier*, puis choisissez `material-margins`.

7. Vérifiez que vous voyez les fichiers et dossiers suivants dans VS Code :
  
    - `requirements.txt`  
    - le dossier `config`
    - le dossier `docs`  
    - le dossier `overrides`

{{< alert title="Utilisateurs avancés : méthode tout en ligne de commande" color="success" >}}

Si vous êtes à l'aise avec le terminal, vous pouvez faire :

``` bash
cd /chemin/vers/le/dossier/destination
git clone https://github.com/technical-margins/material-margins.git
cd material-margins
code .
```

*Assurez-vous que la commande `code` est disponible (ajoutée au PATH) pour ouvrir VS Code depuis le terminal.*

{{< /alert >}}

## Étape 2 : Préparer votre environnement

Vous allez configurer un environnement Python isolé pour installer les dépendances nécessaires au projet sans affecter votre système.

1. Après avoir ouvert le projet material-margins dans VS Code, ouvrez le terminal intégré à VS Code :
   *Terminal > Nouveau terminal*

2. Créez l'environnement virtuel Python :

    ``` bash
    python -m venv .venv
    ```

3. Activez l'environnement virtuel :

    - sous macOS/Linux :

       ``` bash
       source .venv/bin/activate
       ```

    - sous Windows (PowerShell) :

      ``` sh
      .venv\Scripts\Activate.ps1
      ```

4. Vérifiez que l'environnement est activé : vous devez voir `(.venv)` au début de la ligne de commande dans le terminal.

5. Installez les dépendances du projet :

    ``` bash
    pip install -r requirements.txt
    ```

6. Résultat attendu :

    - L'environnement virtuel est activé.
    - Les dépendances (comme MkDocs, Material, etc.) sont installées.

{{< alert title="Utilisateurs avancés : méthode tout en ligne de commande" color="success" >}}

Depuis un terminal, sans passer par VS Code :

``` bash
cd material-margins
python -m venv .venv
source .venv/bin/activate  # Sur Windows : .venv\Scripts\activate
pip install -r requirements.txt
code .
```

{{< /alert >}}

## Étape 3 : Créer un fichier d'article

Vous allez créer le fichier Markdown qui contiendra le contenu de votre article.

1. Dans VS Code, ouvrez le dossier : `docs/fr/blog/posts/`

2. Faites un clic droit sur le dossier `posts` et sélectionnez *Nouveau fichier*.

3. Entrez le nom du fichier, par exemple : `mon-premier-article.md`

4. Vérifiez que le fichier apparaît bien dans l'explorateur VS Code sous `docs/fr/blog/posts/`

{{< alert title="Utilisateurs avancés : méthode alternative en ligne de commande" color="success" >}}

Pour les utilisateurs avancés, il est possible de créer le fichier directement depuis le terminal :

``` bash
touch docs/fr/blog/posts/mon-premier-article.md
```

{{< /alert >}}

## Étape 4 : Ajouter les métadonnées et le contenu

Vous allez structurer votre article et définir les informations nécessaires à son affichage correct dans le blog.

1. Ouvrez le fichier `mon-premier-article.md` dans VS Code.

2. Ajoutez les éléments suivants dans le fichier :

    ```markdown
    ---
    date:
      created: 2025-05-07
    comments: true
    authors:
      - TheMarginWriter
    slug: my-first-post
    categories:
      - Réflexions personnelles
    tags:
      - Apprentissage
      - MkDocs
      - Tutoriel
    ---

    # Mon premier article sur Technical Margins

    Ceci est mon premier article sur *Technical Margins*. Dans cet article, je partage...

    <!-- more -->

    ## Introduction

    Votre introduction ici...

    ## Partie principale

    Le cœur de votre contenu ici...

    <figure markdown="1">
    ![Texte alternatif de l'image](https://example.com/chemin/vers/image.jpg)
    </figure>

    ## Conclusion

    Votre conclusion ici...
    ```

3. Vérifiez que vous utilisez des liens absolus pour les images, hébergées en externe (par exemple sur DeviantArt), afin d'alléger le dépôt.

4. Vérifiez que le champ `date.created` est renseigné correctement (dans les métadonnées en haut de la page). Il détermine la date d'affichage et l'URL de l'article, par exemple `/blog/2025/05/07/...`.

5. Spécifiez un `slug` pour l'article. Bien que ce champ soit facultatif, il est recommandé dans ce projet :

    - Le slug définit le segment final de l'URL de l'article (exemple : `my-first-post`).
    - Il doit être en minuscules, sans accents ni espaces (utilisez des tirets).
    - Dans ce blog multilingue, le slug est utilisé pour synchroniser les URL entre les versions linguistiques d'un même article.

  {{< alert title="Exemple" color="secondary" >}}

  URL générée automatiquement :

  ```
  https://technical-margins.github.io/material-margins/fr/blog/2025/05/07/my-first-post/
  ```
  {{< /alert >}}

6. Rédigez et finalisez le contenu de l'article :

    - Remplacez le texte d'exemple dans les sections *Introduction*, *Partie principale* et *Conclusion* par votre propre contenu.
    - Ajoutez des images pertinentes, des extraits de code ou tout autre élément utile.
    - Vérifiez que votre article est structuré de manière logique et qu'il apporte une information claire ou une réflexion utile au lecteur.
    - Relisez attentivement pour corriger les fautes de grammaire, d'orthographe ou de typographie.

7. Si vous travaillez dans une autre langue, créez le fichier dans le dossier et le dépôt correspondant :

    - Français : `docs/fr/blog/posts/`
    - Anglais : `docs/en/blog/posts/`
    - Chinois simplifié : `docs/zh-cn/blog/posts/`
    - Chinois traditionnel : `docs/zh-tw/blog/posts/`
    - Japonais : `docs/ja/blog/posts/`

{{< alert title="Fonctionnement automatique du blog" color="info" >}}

Notez qu'il n'est pas nécessaire de modifier le fichier `mkdocs.yml` pour que l'article apparaisse dans le blog. Le thème Material détecte automatiquement les articles de blog et génère l'URL en fonction de la date et du slug.

{{< /alert >}}

## Étape 5 : Prévisualiser votre article

Vous allez lancer un serveur local pour vérifier l'apparence et le bon fonctionnement de votre article avant publication.

1. Dans VS Code, ouvrez le terminal intégré si nécessaire :
  *Terminal > Nouveau terminal*

2. Vérifiez que l'environnement virtuel est bien activé. Vous devez voir `(.venv)` au début de la ligne de commande. Si ce n'est pas le cas, activez-le manuellement.

  {{< alert title="Rappel" color="success" >}}
  - sous macOS/Linux :

  ```bash
  source .venv/bin/activate
  ```

  - sous Windows (PowerShell) :

  ```bash
  .venv\Scripts\Activate.ps1
  ```
  {{< /alert >}}

1. Démarrez le serveur local avec la configuration française en saisissant la commande suivante dans le terminal :

    ``` bash
    mkdocs serve -f config/fr/mkdocs.yml
    ```

2. Dans votre navigateur, accédez à : [http://localhost:8000/](http://localhost:8000)

3. Vérifiez que votre article apparaît bien dans la section *Blog* et que son contenu est correctement formaté.

{{< alert title="Limitation locale au niveau des langues" color="warning" >}}

Vous ne pouvez servir qu'un seul site à la fois en local.  
Pour prévisualiser une autre langue, relancez `mkdocs serve` avec le fichier de configuration adapté, par exemple :

``` bash
mkdocs serve -f config/en/mkdocs.yml
```

{{< /alert >}}

## Étape 6 : Commiter et pousser vos changements

Vous allez enregistrer vos modifications dans Git et les envoyer sur GitHub pour les préparer à la publication.

1. Dans VS Code, ouvrez le terminal intégré.

2. Ajoutez le fichier à l'index Git :

    ``` bash
    git add docs/fr/blog/posts/mon-premier-article.md
    ```

3. Enregistrez le commit :

    ``` bash
    git commit -m "Ajout de mon premier article"
    ```

4. Poussez les modifications sur la branche principale :

    ``` bash
    git push origin main
    ```

## Étape 7 : Vérifier l'article publié

Vous allez consulter le site en ligne pour vérifier que votre article est bien publié et affiché comme prévu.

1. Ouvrez l'URL suivante dans votre navigateur : [https://technical-margins.github.io/material-margins/](https://technical-margins.github.io/material-margins/)  

2. Vérifiez que votre article apparaît bien dans la section *Blog* avec les images et la structure attendues.

{{< alert title="Redirection multilingue" color="info" >}}

Le fichier `index.html` à la racine détecte automatiquement la langue de votre navigateur et redirige vers la bonne version du site (`/en/`, `/fr/`, `/ja/`, `/zh-cn/` ou `/zh-tw/`).

{{< /alert >}}

## Et après ?

Maintenant que vous avez publié votre premier article, pourquoi ne pas :

- Expérimenter avec des mises en forme plus riches ([tableaux](https://squidfunk.github.io/mkdocs-material/reference/data-tables/), [diagrammes](https://squidfunk.github.io/mkdocs-material/reference/diagrams/)...)
- Ajouter des [blocs de code](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/) avec coloration syntaxique
- Insérer des éléments interactifs comme des [admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/) (comme celles de ce tutoriel !)

Félicitations pour votre premier article publié sur *Technical Margins* :material-party-popper:
