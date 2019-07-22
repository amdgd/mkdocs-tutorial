---
title: Getting Started
author: Ankit M
date: 2019-07-18
status: draft
---

# Getting Started

### Project Layout

```python
mkdocs.yml                     # Configuration file
.gitignore                     # exclude site/ 
docs/
    CNAME                      # Optional custom domain name
    assets/images/favicon.ico  # favicon file
    images/owls.png            # logo file
    index.md                   # Website homepage
    ...                        # Markdown pages, images and other files
site/                          # Generated website (not included in repo)
```



### MkDocs Commands

- `mkdocs new [dir-name]` - Create a new project
- `mkdocs serve` - Start the live-reloading docs server
- `mkdocs build` - Build the documentation site
- `mkdocs help` - Print this help message



### Dev Server

MkDocs comes with a built-in dev-server that lets you preview your documentation as you work on it. Make sure you're in the same directory as the `mkdocs.yml` configuration file, and then start the server by running the `mkdocs serve` command:

```shell
$ mkdocs serve
>
INFO    -  Building documentation...
INFO    -  Cleaning site directory
[I 190717 23:25:25 server:296] Serving on http://127.0.0.1:8000
[I 190717 23:25:25 handlers:62] Start watching changes
[I 190717 23:25:25 handlers:64] Start detecting changes
```

Open up `http://127.0.0.1:8000/` in your browser, and you'll see the default home page being displayed:



![The MkDocs live server](../img/screenshot-20190717233248757.png)



## Configuration file (mkdocs.yml)

The setup is completely done in a `mkdocs.yml` file within your project's root directory.

In the main folder, open the configuration file: `mkdocs.yml` to make few changes.

It's a YAML file. For a one minute tutorial, check this  [YML Cheatsheet](../cheatsheets/yaml-cheatsheet.md) 

```yaml
site: Your Site name
description: A book to learn MkDocs. 
author: Ankit M
copyright: Copyright &copy; 2016 - 2019.
nav: 
	- Home: home.md
	- About: about.md
```

While the `site` is used as heading the `description` and `author` goes into the meta data. And the `copyright` line will be displayed in the footer.

The navigation may be auto detected or defined using a navigation structure:

```
nav: 
	- Home: home.md
	- About: about.md
  - Languages:
      - Overview: lang/README.md
      - Markdown: lang/markdown.m
      - Handlebars: lang/handlebars.md
```

Read more about Navigation in [Creating Content](creating-content.md)



### Favicon

By default, MkDocs uses the MkDocs favicon. To use a different icon, create an `img` subdirectory in your `docs`directory and copy your custom `favicon.ico` file to that directory. MkDocs will automatically detect and use that file as your favicon icon.



### Theming

Changing the theme is as simple as adding a new variable in mkdocs.yml file. 

Change the configuration filend add a`theme` setting:

```yaml
site_name: MkLorum
nav:
    - Home: index.md
    - About: about.md
theme: readthedocs
```



### Building the site

That's looking good. You're ready to deploy the first pass of your `MkLorum` documentation. First build the documentation:

```shell
$ mkdocs build
```

This will create a new directory, named `site`. Take a look inside the directory:

```shell
$ tree site
site
├── 404.html
├── css
│   ├── base.css
│   ├── bootstrap-custom.min.css
│   └── font-awesome.min.css
├── fonts
│   ├── fontawesome-webfont.eot
│   ├── fontawesome-webfont.svg
│   ├── fontawesome-webfont.ttf
│   ├── fontawesome-webfont.woff
│   ├── fontawesome-webfont.woff2
│   ├── glyphicons-halflings-regular.eot
│   ├── glyphicons-halflings-regular.svg
│   ├── glyphicons-halflings-regular.ttf
│   ├── glyphicons-halflings-regular.woff
│   └── glyphicons-halflings-regular.woff2
├── getting-started
│   └── index.html
├── img
│   ├── favicon.ico
│   ├── grid.png
│   └── screenshot-20190717233248757.png
├── index.html
├── js
│   ├── base.js
│   ├── bootstrap-3.0.3.min.js
│   └── jquery-1.10.2.min.js
├── search
│   ├── lunr.js
│   ├── main.js
│   ├── search_index.json
│   └── worker.js
├── sitemap.xml
├── sitemap.xml.gz
└── yaml-cheatsheet
    └── index.html
```



Notice that your source documentation has been output as two HTML files named `index.html` `and getting-started/index.html`. 

You also have various other media that's been copied into the `site` directory as part of the documentation theme. You even have a `sitemap.xml` file and `mkdocs/search_index.json`.

If you're using source code control such as `git` you probably don't want to check your documentation builds into the repository. Add a line containing `site/` to your `.gitignore` file.

```shell
$ echo "site/" >> .gitignore
```



After some time, files may be removed from the documentation but they will still reside in the `site` directory. To remove those stale files, just run `mkdocs` with the `--clean` switch.

```
mkdocs build --clean
```





## MKDocs Walkthrough

1. Create Repo

2. Install mkdocs

   ```
   virtualenv ve
   source ve/bin/activate
   pip install mkdocs
   ```

3. Init the mkdocs project

   ```
   mkdocs new .
   ```

4. Customize mkdocs.yml

   ```
   site_name: Mkdocs overview
   pages:
     - Home: 'README.md'
   ```

5. Add / Edit pages

6. Run local server

   ```
   mkdocs serve
   ```

7. Edit and revise

8. Commit and push source to github

9. Deploy to gh-pages

   ```
   mkdocs gh-deploy
   ```

10. Profit

## Advanced

### Themes

```
site_name: Mkdocs overview
pages:
  - Home: 'README.md'
theme: readthedocs
```

### Extensions

- Any pyMdown extensions

```
pip install pymdown-extensions
```

http://facelessuser.github.io/pymdown-extensions/

```shell
site_name: Mkdocs overview
pages:
    - Home: 'README.md'
markdown_extensions:
    - pymdownx.superfences
```

