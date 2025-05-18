---
title: "Tutorial: Creating your first blog post"
linkTitle: Tutorial
weight: 10  
type: docs
---

This tutorial guides you through writing and publishing your first blog post on the MkDocs Material blog *Technical Margins*. By the end, you will have written, formatted and published a post with metadata, images and proper structuring.

## Prerequisites

Before starting, ensure you have:

- [Python](https://www.python.org/downloads/) installed on your computer (version 3.12 recommended)  
- [Git](https://git-scm.com/downloads) installed  
- A [GitHub](https://github.com/) account  
- Basic knowledge of [Markdown](https://www.markdownguide.org/) syntax  
- A text editor ([VS Code](https://code.visualstudio.com/download) recommended)  
- Access to the GitHub repository: `technical-margins/material-margins` (🔒 private)

{{< alert title="Recommended extensions for VS Code" color="success" >}}

- **Python** (Microsoft)  
- **Markdownlint** (for editing comfort)

{{< /alert >}}

## Step 1: Clone the repository

This step involves getting a local copy of the project on your computer so you can work offline instead of directly online.

1. Open your file explorer (Windows, Finder, or other).

2. Go to where you want to clone the project, for example `Documents`.

3. Create a folder, for example `MyProjects`.

4. Right-click on this folder and select:

    - on Linux: *Open in terminal*
    - on Windows: *Open in Terminal* or *Open in PowerShell*
    - on macOS: *New Terminal at Folder* (via *Finder > Services*; activate if needed in System Preferences)

5. Clone the repository by typing the command:

    ``` bash
    git clone https://github.com/technical-margins/material-margins.git
    ```

6. Open VS Code and select:
   *File > Open Folder*, then choose `material-margins`.

7. Check that you see the following files and folders in VS Code:
  
    - `requirements.txt`  
    - the `config` folder
    - the `docs` folder  
    - the `overrides` folder

{{< alert title="Advanced users: command line method" color="success" >}}

If you're comfortable with the terminal, you can do:

``` bash
cd /path/to/destination/folder
git clone https://github.com/technical-margins/material-margins.git
cd material-margins
code .
```

*Ensure the `code` command is available (added to PATH) to open VS Code from the terminal.*

{{< /alert >}}

## Step 2: Prepare your environment

Here you'll set up an isolated Python environment to install all necessary dependencies without affecting your system settings.

1. After opening the material-margins project in VS Code, open the integrated terminal:
   *Terminal > New Terminal*

2. Create the Python virtual environment:

    ``` bash
    python -m venv .venv
    ```

3. Activate the virtual environment:

    - on macOS/Linux:

       ``` bash
       source .venv/bin/activate
       ```

    - on Windows (PowerShell):

      ``` sh
      .venv\Scripts\Activate.ps1
      ```

4. Verify that the environment is activated: you should see `(.venv)` at the beginning of the command line in the terminal.

5. Install the project dependencies:

    ``` bash
    pip install -r requirements.txt
    ```

6. Expected result:

    - The virtual environment is activated.
    - The dependencies (such as MkDocs, Material, etc.) are installed.

{{< alert title="Advanced users: command line method" color="success" >}}

From a terminal, without using VS Code:

``` bash
cd material-margins
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
code .
```

{{< /alert >}}

## Step 3: Create a blog post file

In this step, we'll create the Markdown file that will hold your post's content.

1. In VS Code, open the folder: `docs/en/blog/posts/`

2. Right-click on the `posts` folder and select *New File*.

3. Enter the filename, for example: `my-first-post.md`

4. Verify that the file appears in the VS Code explorer under `docs/en/blog/posts/`

{{< alert title="Advanced users: alternative method using command line" color="success" >}}

For advanced users, it's possible to create the file directly from the terminal:

``` bash
touch docs/en/blog/posts/my-first-post.md
```

{{< /alert >}}

## Step 4: Add metadata and content

Now it's time to structure your post and add the required information for proper display in the blog.

1. Open the `my-first-post.md` file in VS Code.

2. Add the following elements into the file:

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

3. Ensure you use absolute links for images, hosted externally (for example on DeviantArt), to keep the repository lightweight.

4. Verify that the `date.created` field is filled in correctly (in the metadata at the top of the page). It determines the display date and URL of the post, for example `/blog/2025/05/07/...`.

5. Specify a `slug` for the post. Although this field is optional, it is recommended in this project:

    - The slug defines the final segment of the post's URL (example: `my-first-post`).
    - It should be lowercase, without accents or spaces (use hyphens).
    - In this multilingual blog, the slug is used to synchronise URLs between language versions of the same post.

  {{< alert title="Example" color="secondary" >}}

  Automatically generated URL:

  ```
  https://technical-margins.github.io/material-margins/en/blog/2025/05/07/my-first-post/
  ```

  {{< /alert >}}

6. Write and edit your article content:

    - Replace the placeholder text in the *Introduction*, *Main section*, and *Conclusion* with your actual content.
    - Add relevant images, code examples, or other media as needed.
    - Ensure your article flows logically and provides value to readers.
    - Proofread your content for spelling and grammatical errors.

7. If you're working in another language, create the file in the corresponding folder and repository:

    - French: `docs/fr/blog/posts/`
    - English: `docs/en/blog/posts/`
    - Simplified Chinese: `docs/zh-cn/blog/posts/`
    - Traditional Chinese: `docs/zh-tw/blog/posts/`
    - Japanese: `docs/ja/blog/posts/`

{{< alert title="Automatic blog functioning" color="info" >}}

Note that it is not necessary to modify the `mkdocs.yml` file for the post to appear in the blog. The Material theme automatically detects blog posts and generates the URL based on the date and slug.

{{< /alert >}}

## Step 5: Preview your post

Before publishing, this step shows you how to launch a local server to check how your post looks and functions.

1. In VS Code, open the integrated terminal if necessary:
  *Terminal > New Terminal*

2. Check that the virtual environment is activated. You should see `(.venv)` at the beginning of the command line. If not, activate it manually.

  {{< alert title="Reminder" color="success" >}}

  - on macOS/Linux:

  ```bash
  source .venv/bin/activate
  ```

  - on Windows (PowerShell):

  ```bash
  .venv\Scripts\Activate.ps1
  ```

  {{< /alert >}}

3. Start the local server with the English configuration by entering the following command in the terminal:

    ``` bash
    mkdocs serve -f config/en/mkdocs.yml
    ```

4. In your browser, go to: [http://localhost:8000/](http://localhost:8000)

5. Check that your post appears in the *Blog* section and that its content is correctly formatted.

{{< alert title="Local language limitation" color="warning" >}}

You can only serve one site at a time locally.  
To preview another language, restart `mkdocs serve` with the appropriate configuration file, for example:

``` bash
mkdocs serve -f config/fr/mkdocs.yml
```

{{< /alert >}}

## Step 6: Commit and push your changes

This is where you'll save your work in Git and upload it to GitHub in preparation for publication.

1. In VS Code, open the integrated terminal.

2. Add the file to the Git index:

    ``` bash
    git add docs/en/blog/posts/my-first-post.md
    ```

3. Save the commit:

    ``` bash
    git commit -m "Add my first post"
    ```

4. Push the changes to the main branch:

    ``` bash
    git push origin main
    ```

## Step 7: Check the published post

Finally, we'll visit the online site to confirm your post appears as intended.

1. Open the following URL in your browser: [https://technical-margins.github.io/material-margins/](https://technical-margins.github.io/material-margins/)

2. Check that your post appears in the *Blog* section with the expected images and structure.

{{< alert title="Multilingual redirection" clor="info" >}}

The `index.html` file at the root automatically detects your browser's language and redirects to the correct version of the site (`/en/`, `/fr/`, `/zh-cn/`, `/zh-tw/`, or `/ja/`).

{{< /alert >}}

## What next?

Now that you've published your first post, why not:

- Experiment with richer formatting ([tables](https://squidfunk.github.io/mkdocs-material/reference/data-tables/), [diagrams](https://squidfunk.github.io/mkdocs-material/reference/diagrams/)...)
- Add [code blocks](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/) with syntax highlighting
- Insert interactive elements like [admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/) (like those in this tutorial!)

Congratulations on your first post published on *Technical Margins*!