---
title: Creating Content
author: Ankit M
date: 2019-07-18
status: draft
---

# Creating Content

## File layout

Your documentation source should be written as regular Markdown files, and placed in `docs` directory. By default, this directory will be named `docs` and will exist at the top level of your project, alongside the `mkdocs.yml` configuration file.

The simplest project you can create will look something like this:

```
mkdocs.yml
docs/
    index.md
```

By convention your project homepage should always be named `index`. Any of the following extensions may be used for your Markdown source files: `markdown`, `mdown`, `mkdn`, `mkd`, `md`. All Markdown files included in your documentation directory will be rendered in the built site regardless of any settings.

You can also create multi-page documentation, by creating several Markdown files:

```
mkdocs.yml
docs/
    index.md
    about.md
    license.md
```

The file layout you use determines the URLs that are used for the generated pages. Given the above layout, pages would be generated for the following URLs:

```
/
/about/
/license/
```

You can also include your Markdown files in nested directories if that better suits your documentation layout.

```
docs/
    index.md
    user-guide/getting-started.md
    user-guide/configuration-options.md
    license.md
```

Source files inside nested directories will cause pages to be generated with nested URLs, like so:

```
/
/user-guide/getting-started/
/user-guide/configuration-options/
/license/
```

## Index pages

When a directory is requested, by default, most web servers will return an index file (usually named `index.html`) contained within that directory if one exists. For that reason, the homepage in all of the examples above has been named `index.md`, which MkDocs will render to `index.html` when building the site.

Many repository hosting sites provide special treatment for README files by displaying the contents of the README file when browsing the contents of a directory. Therefore, MkDocs will allow you to name your index pages as `README.md` instead of `index.md`. In that way, when users are browsing your source code, the repository host can display the index page of that directory as it is a README file. However, when MkDocs renders your site, the file will be renamed to `index.html` so that the server will serve it as a proper index file.

If both an `index.md` file and a `README.md` file are found in the same directory, then the `index.md` file is used and the `README.md` file is ignored.



## Navigation

You can change navigation in `mkdocs.yml` file located in the root directory of the project folder.

This setting is used to determine the format and layout of the global navigation for the site. For example, the following would create "Introduction", "User Guide" and "About" navigation items.

```
nav:
    - 'Introduction': 'index.md'
    - 'User Guide': 'user-guide.md'
    - 'About': 'about.md'
```



### External Links

Navigation items may also include links to external sites. While titles are optional for internal links, they are required for external links. An external link may be a full URL or a relative URL. Any path which is not found in the files is assumed to be an external link.

```
nav:
    - Home: index.md
    - User Guide: user-guide.md
    - Bug Tracker: https://example.com/
```



### When Mkdocs is hosted in sub-directory

However, sometimes the MkDocs site is hosted in a subdirectory of a project's site and you may want to link to other parts of the same site without including the full domain. In that case, you may use and appropriate relative URL.

```
site_url: https://example.com/foo/

nav:
    - Home: ../
    - User Guide: user-guide.md
    - Bug Tracker: /bugs/
```

Note: Derent styles of external links are used. 

- First note that the `site_url` indicates that the MkDocs site is hosted in the `/foo/` subdirectory of the domain. Therefore, the `Home` navigation item is a relative link which steps up one level to the server root and effectively points to `https://example.com/`. 
- The `Bug Tracker` item uses an absolute path from the server root and effectively points to `https://example.com/bugs/`. 
- Of course, the `User Guide` points to a local MkDocs page.



### Ordering of Nav Items

By default `nav` will contain an alphanumerically sorted, nested list of all the Markdown files found within the `docs_dir` and its sub-directories. 

If none are found it will be `[]` (an empty list).



### Sub-sections

Navigation sub-sections can be created by listing related pages together under a section title. For example:

```
nav:
- Home: 'index.md'
- User Guide:
    - 'Writing your docs': 'writing-your-docs.md'
    - 'Styling your docs': 'styling-your-docs.md'
- About:
    - 'License': 'license.md'
    - 'Release Notes': 'release-notes.md'
```

With the above configuration we have three top level items: "Home", "User Guide" and "About." "Home" is a link to the homepage for the site. Under the "User Guide" section two pages are listed: "Writing your docs" and "Styling your docs." Under the "About" section two more pages are listed: "License" and "Release Notes."

Note that a section cannot have a page assigned to it. Sections are only containers for child pages and sub-sections. You may nest sections as deeply as you like. However, be careful that you don't make it too difficult for your users to navigate through the site navigation by over-complicating the nesting. While sections may mirror your directory structure, they do not have to.



### Hidden Pages

Any pages not listed in your navigation configuration will still be rendered and included with the built site, however, they will not be linked from the global navigation and will not be included in the `previous` and `next` links. Such pages will be "hidden" unless linked to directly.



## Meta Data / Front Matter

MkDocs includes support for both YAML and MultiMarkdown style meta-data (often called front-matter). 

Meta-data consists of a series of keywords and values defined at the beginning of a Markdown document, which are stripped from the document prior to it being processing by Python-Markdown. 

The key/value pairs are passed by MkDocs to the page template. Therefore, if a theme includes support, the values of any keys can be displayed on the page or used to control the page rendering.

In addition to displaying information in a template, MkDocs includes support for a few predefined meta-data keys which can alter the behavior of MkDocs for that specific page. The following keys are supported:

### template

The template to use with the current page.By default, MkDocs uses the `main.html` template of a theme to render Markdown pages. You can use the `template` meta-data key to define a different template file for that specific page. The template file must be available on the path(s) defined in the theme's environment.

### title

The "title" to use for the document.

MkDocs will attempt to determine the title of a document in the following ways, in order:

1. A title defined in the nav configuration setting for a document.
2. A title defined in the `title` meta-data key of a document.
3. A level 1 Markdown header on the first line of the document body.
4. The filename of a document.

Upon finding a title for a page, MkDoc does not continue checking any additional sources in the above list.



### YAML style meta-data

YAML style meta-data consists of YAML key/value pairs wrapped in YAML style deliminators to mark the start and/or end of the meta-data. The first line of a document must be `---`. The meta-data ends at the first line containing an end deliminator (either `---` or `...`). The content between the deliminators is parsed as YAML

 [Yaml Cheatsheet](yaml-cheatsheet.md) 

```yaml
---
title: Getting Started
authors:
    - Waylan Limberg
    - Tom Christie
date: 2018-07-10
some_url: https://example.com
status: draft
---
```

