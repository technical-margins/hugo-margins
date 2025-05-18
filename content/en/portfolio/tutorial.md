---
title: "Tutorial: Creating your first blog post"
linkTitle: Tutorial
weight: 10  
type: docs
---

This tutorial guides you through writing and publishing your first blog post on the MkDocs Material blog *Technical Margins*. By the end, you will have written, formatted and published a post with metadata, images and proper structuring.

## Prerequisites

Before starting, ensure you have:

- [Python](https://www.python.org/downloads) (version 3.12 recommended)  
- [Git](https://git-scm.com/downloads)  
- A [GitHub](https://github.com/) account  
- Basic knowledge of [Markdown](https://www.markdownguide.org/)  
- A text editor ([VS Code](https://code.visualstudio.com/download) recommended)  

{{< alert title="Tip" color="success" >}}
Recommended VS Code extensions:
- **Python** (Microsoft)  
- **Markdownlint** (for editing comfort)  
{{< /alert >}}

You must also have access to the GitHub repository: `technical-margins/material-margins`.

## Step 1: Clone the repository

1. Open your file explorer.
2. Navigate to your desired project folder, e.g. `Documents/MyProjects`.
3. Right-click and select:

   - Linux: *Open in Terminal*
   - Windows: *Open in PowerShell*
   - macOS: *New Terminal at Folder*

4. Run:

    ```bash
    git clone https://github.com/technical-margins/material-margins.git
    ```

5. Open VS Code: *File > Open Folder*, then select `material-margins`.

6. You should see:

    - `requirements.txt`
    - `config/`
    - `docs/`
    - `overrides/`

{{< alert title="Tip for advanced users" color="success" >}}
From the command line:

```bash
cd /path/to/folder
git clone https://github.com/technical-margins/material-margins.git
cd material-margins
code .
```

Ensure `code` is in your PATH.
{{< /alert >}}

## Step 2: Prepare your environment

1. In VS Code: *Terminal > New Terminal*

2. Create a virtual environment:

   ```bash
   python -m venv .venv
   ```

3. Activate it:

   * macOS/Linux:

     ```bash
     source .venv/bin/activate
     ```

   * Windows (PowerShell):

     ```sh
     .venv\Scripts\Activate.ps1
     ```

4. Check the `(.venv)` prefix in the terminal prompt.

5. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

{{< alert title="CLI-only alternative" color="success" >}}

From the command line:

```bash
cd material-margins
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
code .
```

{{< /alert >}}

## Step 3: Create a blog post file

1. In VS Code, open `docs/en/blog/posts/`.
2. Right-click `posts/` → *New File* → `my-first-post.md`.

{{< alert title="CLI-only alternative" color="success" >}}

From the command line:

```bash
touch docs/en/blog/posts/my-first-post.md
```

{{< /alert >}}

## Step 4: Add metadata and content

Open `my-first-post.md` and insert:

```markdown
---
date:
  created: 2025-05-07
comments: true
authors:
  - TheMarginWriter
slug: my-first-post
categories:
  - Personal reflections
tags:
  - Learning
  - MkDocs
  - Tutorial
---

# My first post on Technical Margins

This is my first post on *Technical Margins*. In this post, I share...

<!-- more -->

## Introduction

Your introduction here...

## Main section

The core of your content here...

<figure markdown="1">
![Alternative text for the image](https://example.com/path/to/image.jpg)
</figure>

## Conclusion

Your conclusion here...
```

* Use **absolute URLs** for images.
* The `slug` defines the post's final URL segment.
* `<!-- more -->` controls the preview summary on blog listing pages.

{{< alert title="Multilingual structure" color="info" >}}
Place files in the correct subfolder:

* French: `docs/fr/blog/posts/`
* English: `docs/en/blog/posts/`
* Simplified Chinese: `docs/zh-cn/blog/posts/`
* Traditional Chinese: `docs/zh-tw/blog/posts/`
* Japanese: `docs/ja/blog/posts/`
  {{< /alert >}}

## Step 5: Preview your post

1. Ensure `(.venv)` is active in terminal.

2. Run:

   ```bash
   mkdocs serve -f config/en/mkdocs.yml
   ```

3. Open [http://localhost:8000/](http://localhost:8000/) in your browser.

{{< alert title="Local language preview" color="info" >}}
To preview another language:

```bash
mkdocs serve -f config/fr/mkdocs.yml
```

{{< /alert >}}

## Step 6: Commit and push your changes

```bash
git add docs/en/blog/posts/my-first-post.md
git commit -m "Add my first post"
git push origin main
```

## Step 7: Check the published post

Visit:

```sh
https://technical-margins.github.io/material-margins/
```

Check your post under *Blog*.

{{< alert title="Multilingual redirection" color="info" >}}

The root `index.html` detects your browser's language and redirects to `/en/`, `/fr/`, `/zh-cn/`, `/zh-tw/`, or `/ja/`.

{{< /alert >}}

## What next?

Now that your first post is live, try:

* Using richer formatting like [tables](https://squidfunk.github.io/mkdocs-material/reference/data-tables/)
* Adding [code blocks](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/)
* Inserting [admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/) or diagrams

Enjoy blogging on *Technical Margins* 🎉
