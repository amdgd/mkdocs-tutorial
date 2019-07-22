---
title: Markdown Cheatsheet
author: Ankit M
date: 2019-07-18
status: draft
---

# Extensions & Plugins

## Installing Plugins

Before a plugin can be used, it must be installed on the system. If you are using a plugin which comes with MkDocs, then it was installed when you installed MkDocs. However, to install third party plugins, you need to determine the appropriate package name and install it using `pip`:

```shell
$ pip install mkdocs-foo-plugin
```

## Using Plugins

The  `plugins` configuration option should contain a list of plugins to use when building the site. Each "plugin" must be a string name assigned to the plugin (see the documentation for a given plugin to determine its "name"). A plugin listed here must already be instlled.

```yaml
plugins:
    - search
```

Some plugins may provide configuration options of their own. If you would like to set any configuration options, then you can nest a key/value mapping (`option_name: option value`) of any options that a given plugin supports. Note that a colon (`:`) must follow the plugin name and then on a new line the option name and value must be indented and separated by a colon. If you would like to define multiple options for a single plugin, each option must be defined on a separate line.

```yaml
plugins:
    - search:
        lang: en
        foo: bar
```

### Markdown extensions

MkDocs uses the [Python Markdown](https://python-markdown.github.io/) library to translate Markdown files into HTML. Python Markdown supports a variety of [extensions](https://python-markdown.github.io/extensions/)that customize how pages are formatted. This setting lets you enable a list of extensions beyond the ones that MkDocs uses by default 

Default MkDocs extensions

- `meta`
-  `toc`
- `tables`
- `fenced_code`



To enable an extension - use this format in mkdocs.yaml

```yaml
markdown_extensions:
    - codehilite
    - markdown_include.include
```



| Extension                                                    | Entry Point   | Description                                                  |
| :----------------------------------------------------------- | :------------ | :----------------------------------------------------------- |
| [Extra](https://python-markdown.github.io/extensions/extra/) | `extra`       | A compilation of various Python-Markdown extensions that (mostly) imitates PHP Markdown Extra. |
| [Abbreviations](https://python-markdown.github.io/extensions/abbreviations/) | `abbr`        | The Abbreviations extension adds the ability to define abbreviations. Specifically, any defined abbreviation is wrapped in an `<abbr>` tag. |
| [Attribute Lists](https://python-markdown.github.io/extensions/attr_list/) | `attr_list`   | The Attribute Lists extension adds a syntax to define attributes on the various HTML elements in markdown’s output. |
| [Definition Lists](https://python-markdown.github.io/extensions/definition_lists/) | `def_list`    | The Definition Lists extension adds the ability to create definition lists in Markdown documents. |
| [Fenced Code Blocks](https://python-markdown.github.io/extensions/fenced_code_blocks/) | `fenced_code` | The Fenced Code Blocks extension adds a secondary way to define code blocks, which overcomes a few limitations of the indented code blocks. |
| [Footnotes](https://python-markdown.github.io/extensions/footnotes/) | `footnotes`   | The Footnotes extension adds syntax for defining footnotes in Markdown documents. |
| [Tables](https://python-markdown.github.io/extensions/tables/) | `tables`      | The Tables extension adds the ability to create tables in Markdown documents. |
| [Admonition](https://python-markdown.github.io/extensions/admonition/) | `admonition`  | The Admonition extension adds [rST-style](http://docutils.sourceforge.net/docs/ref/rst/directives.html#specific-admonitions) admonitions to Markdown documents. |
| [CodeHilite](https://python-markdown.github.io/extensions/code_hilite/) | `codehilite`  | The CodeHilite extension adds code/syntax highlighting to standard Python-Markdown code blocks using [Pygments](http://pygments.org/). |
| [Legacy Attributes](https://python-markdown.github.io/extensions/legacy_attr/) | `legacy_attr` | Legacy Attributes extension restores Python-Markdown’s original attribute setting syntax. |
| [Legacy Emphasis](https://python-markdown.github.io/extensions/legacy_em/) | `legacy_em`   | The Legacy EM extension restores Markdown’s original behavior for emphasis and strong syntax when using underscores. |
| [Meta-Data](https://python-markdown.github.io/extensions/meta_data/) | `meta`        | The Meta-Data extension adds a syntax for defining meta-data about a document. |
| [New Line to Break](https://python-markdown.github.io/extensions/nl2br/) | `nl2br`       | The New-Line-to-Break (`nl2br`) Extension will cause newlines to be treated as hard breaks; like StackOverflow and [GitHub](http://github.github.com/github-flavored-markdown/) flavored Markdown do. |
| [Sane Lists](https://python-markdown.github.io/extensions/sane_lists/) | `sane_lists`  | The Sane Lists extension alters the behavior of the Markdown List syntax to be less surprising. |
| [SmartyPants](https://python-markdown.github.io/extensions/smarty/) | `smarty`      | The SmartyPants extension converts ASCII dashes, quotes and ellipses to their HTML entity equivalents. |
| [Table of Contents](https://python-markdown.github.io/extensions/toc/) | `toc`         | The Table of Contents extension generates a Table of Contents from a Markdown document and adds it into the resulting HTML document. |
| [WikiLinks](https://python-markdown.github.io/extensions/wikilinks/) | `wikilinks`   | The WikiLinks extension adds support for [WikiLinks](http://en.wikipedia.org/wiki/Wikilink). Specifically, any `[[bracketed]]` word is converted to a link |



## PyMdown Extensions

[PyMdown Extensions](http://facelessuser.github.io/pymdown-extensions/) is a collection of Markdown extensions that add some great features to the standard Markdown library. For this reason, the **installation of this package is highly recommended** as it's well-integrated with the Material theme.

The PyMdown Extensions package can be installed with the following command:

```shell
$ pip install pymdown-extensions
```



The following list of extensions that are part of the PyMdown Extensions package are recommended to be used together with the Material theme:

```yaml
markdown_extensions:
  - pymdownx.arithmatex
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.critic
  - pymdownx.details
  - pymdownx.emoji:
      emoji_generator: !!python/name:pymdownx.emoji.to_svg
  - pymdownx.inlinehilite
  - pymdownx.magiclink
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde
```



### Python-Markdown Github-Links Extension

An extension to Python-Markdown which adds support for shorthand links to GitHub users, repositories, issues and commits.

To install the extension run the following command:

```shell
$ pip install mdx-gh-links
```
@{ankitind}

@{user} to link to a user or organization and @{user}/{repo} to link

df

df



What would you drink, :fa-coffee: or :fa-beer:?