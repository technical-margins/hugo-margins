---
title: "Guide pratique : Prévisualiser le site MkDocs multilingue avec Docker"
linkTitle: Guide pratique
weight: 20  
type: docs
---

Ce guide explique comment tester localement le site multilingue complet de *Technical Margins*, y compris la détection automatique de la langue et la navigation entre les versions.

## Quand l'utiliser

Utilisez ce guide si vous travaillez sur *Technical Margins* ou un projet similaire, c'est-à-dire :

- Un site MkDocs multilingue organisé par dossiers (`/fr`, `/en`, etc.) et avec différents fichiers de configuration.
- Sans utilisation du plugin [i18n](https://ultrabug.github.io/mkdocs-static-i18n/) (par souci de compatibilité avec la fonction blog).
- Avec un besoin de vérifier la redirection automatique et la navigation multilingue en conditions proches de la production.

## Prérequis

- Docker installé sur votre machine.
- Connaissances de base en ligne de commande.
- Le dépôt cloné et prêt à l'emploi : `technical-margins/material-margins`

## Étape 1 : Construire l'image Docker du site

Depuis la racine du projet, lancez la commande suivante :

```bash
docker build -t technical-margins-site -f docker/margins.Dockerfile .
```

Cette étape :

- Crée une image Docker nommée `technical-margins-site`.
- Exécute les builds MkDocs pour `en`, `fr`, `ja`, `zh-cn`, `zh-tw` (les langues configurées).
- Prépare les fichiers statiques avec les chemins relatifs (`/material-margins/`).  
- Configure un serveur Nginx pour les servir.

{{< alert title="Dockerfile prêt à l'emploi" color="info" >}}
  
Le projet *Technical Margins* inclut un Dockerfile prêt à l'emploi : `docker/margins.Dockerfile`.  

Ce Dockerfile :  

- Utilise l'image `squidfunk/mkdocs-material` pour générer les fichiers HTML.
- Installe les plugins nécessaires (par ex. `mkdocs-glightbox`).
- Copie tout le projet dans `/docs` dans le conteneur.
- Exécute la construction (`mkdocs build`) pour les langues configurées.
- Prépare une image Nginx minimaliste pour servir les fichiers générés.

{{< /alert >}}

## Étape 2 : Lancer le conteneur du site

Démarrez le conteneur avec le bon nom (important pour le proxy) :

```bash
docker run -ti --rm --name material-margins -p 8082:80 technical-margins-site
```

{{< alert title="Attention" color="warning" >}}

Accéder directement à `http://localhost:8082/` ne fonctionnera pas à cause du préfixe `/material-margins/` ajouté par l'index de redirection.

{{< /alert >}}

## Étape 3 : Construire l'image Nginx proxy

Depuis la racine du projet, construisez l'image Nginx :

```bash
docker build -t nginx-proxy-margins -f docker/nginx.Dockerfile .
```

Cette image sert de proxy et redirige correctement les requêtes avec le préfixe `/material-margins/`.

## Étape 4 : Lancer le conteneur Nginx (proxy)

Démarrez le conteneur Nginx et liez-le au conteneur du site :

```bash
docker run -ti --rm --name nginx-material-margins --link material-margins:material-margins -p 8083:80 nginx-proxy-margins
```

## Étape 5 : Vérifier le fonctionnement multilingue

Dans votre navigateur, ouvrez : [http://localhost:8083/material-margins/](http://localhost:8083/material-margins/)

Vérifiez :

1. La redirection automatique selon la langue du navigateur (grâce au script dans `docs/index.html`).
2. La navigation entre les langues (via la page d'accueil).
3. Le bon affichage des pages et des articles dans chaque langue.

## Dépannage

**La redirection échoue ou casse les URLs :**

Vérifiez le fichier `docs/index.html` (script de redirection) et le `nginx.conf` (préfixe `/material-margins/`).

**Le site n'est pas accessible :**

Vérifiez :

- Les conteneurs actifs (`docker ps`) ;
- Le mapping des ports (`8082`, `8083`) ;
- Que le conteneur MkDocs s'appelle bien `material-margins` (nécessaire pour `--link`).

## Conclusion

Grâce à Docker, vous pouvez tester localement l'intégralité de votre site multilingue, dans des conditions proches de la production. Cela vous permet de vérifier la détection de langue, le fonctionnement des redirections et l'expérience utilisateur globale avant déploiement.
