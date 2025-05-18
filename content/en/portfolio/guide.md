---
title: "How-to guide: Preview the multilingual MkDocs site with Docker"
linkTitle: How-to guide
weight: 20  
type: docs
---

This guide explains how to locally test the complete multilingual MkDocs site of *Technical Margins*, including automatic language detection and navigation between versions.

## When to use this

Use this guide if you're working on *Technical Margins* or a similar project, which means:

- A multilingual MkDocs site organised by folders (`/fr`, `/en`, etc.) with different configuration files.
- Without using the [i18n plugin](https://ultrabug.github.io/mkdocs-static-i18n/) (for compatibility with the blog plugin).
- With a need to check automatic redirection and multilingual navigation in conditions close to production.

## Prerequisites

- Docker installed on your machine.
- Basic command line knowledge.
- The repository cloned and ready to use: `technical-margins/material-margins`

## Step 1: Build the site Docker image

From the project root, run the following command:

```bash
docker build -t technical-margins-site -f docker/margins.Dockerfile .
```

This step:

- Creates a Docker image named `technical-margins-site`.
- Runs MkDocs builds for `en`, `fr`, `ja`, `zh-cn`, `zh-tw` (the configured languages).
- Prepares the static files with relative paths (`/material-margins/`).  
- Configures an Nginx server to serve them.

{{< alert title="Ready-to-use Dockerfile" color="info" >}}

The *Technical Margins* project includes a ready-to-use Dockerfile: `docker/margins.Dockerfile`.  

This Dockerfile:  

- Uses the `squidfunk/mkdocs-material` image to generate HTML files.
- Installs necessary plugins (e.g. `mkdocs-glightbox`).
- Copies the entire project into `/docs` in the container.
- Runs builds (`mkdocs build`) for the configured languages.
- Prepares a minimalist Nginx image to serve the generated files.

{{< /alert >}}

## Step 2: Launch the site container

Start the container with the right name (important for the proxy):

```bash
docker run -ti --rm --name material-margins -p 8082:80 technical-margins-site
```

{{< alert title="Caution" color="warning" >}}

Accessing `http://localhost:8082/` directly will not work because of the `/material-margins/` prefix added by the redirection index.

{{< /alert >}}

## Step 3: Build the Nginx proxy image

From the project root, build the Nginx image:

```bash
docker build -t nginx-proxy-margins -f docker/nginx.Dockerfile .
```

This image serves as a proxy and correctly redirects requests with the `/material-margins/` prefix.

## Step 4: Launch the Nginx container (proxy)

Start the Nginx container and link it to the site container:

```bash
docker run -ti --rm --name nginx-material-margins --link material-margins:material-margins -p 8083:80 nginx-proxy-margins
```

## Step 5: Verify multilingual functionality

In your browser, open: [http://localhost:8083/material-margins/](http://localhost:8083/material-margins/)

Check:

1. Automatic redirection based on browser language (thanks to the script in `docs/index.html`).
2. Navigation between languages (via the homepage).
3. Proper display of pages and articles in each language.

## Troubleshooting

**Redirection fails or breaks URLs:**

Check the `docs/index.html` file (redirection script) and the `nginx.conf` (prefix `/material-margins/`).

**The site is not accessible:**

Check:

- Active containers (`docker ps`);
- Port mapping (8082, 8083);
- That the MkDocs container is named `material-margins` (necessary for `--link`).

## Conclusion

Thanks to Docker, you can locally test your entire multilingual site under conditions similar to production. This allows you to verify language detection, check that redirections work properly, and evaluate the overall user experience before deployment.
